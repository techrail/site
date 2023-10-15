---
draft: false
title: Why we need Log Message Identifiers or LMID
tags:
  - blog
  - vaibhav
  - bark
  - logging
  - wiki
aliases:
  - lmid
---
Logging is almost central to software development. Logging is probably more important than coding itself at certain places and times. You need logs to look into the past - to find out what happened - whether it was right or wrong or did someone actually try to steal something from you!? Logs are everywhere. Since the time we software developers learn to code till the point we feel like we have the control over whatever technologies and methodologies we are working on, we use logs to figure out what's happening and what's already happened!

In larger installations and companies, they often have a dedicated _logging infrastructure_ teams which take care of just one aspect - logging. Logging as a discipline of software engineering is pretty vast. When you think about logging on a large scale, you have to think of multiple technologies and disciplines - ingestion, load balancing, databases, search methodologies, storage management and more.

And yet, when we have a problem to debug, oftentimes, we pull our hair in frustration (disclaimer: I do not attribute logging to my balding head 😂). Questions like:

- _who sent this log message?_
- _from where was it sent?_
- _when was it sent?_
- _which user action caused it?_
- _what are the surrounding logs of that one particular log message in that one user's session?_

are very important when you are debugging a nasty bug. It only makes sense to talk about how we can log properly.
## Introduction to the Problem
The biggest problem with logging is created by our own selves - we copy paste code. The intentions are usually noble - we want to copy a well-working code elsewhere to replicate the functionality or to copy it and then modify the behaviour. And while we do that, sometimes (or dare I say most of the times) we leave the log messages in that piece of code untouched. I mean what's the room for innovation in doing a `log.Println("Email address is required")`? But then, if you have copied some sort of code that checks for presence of email in the input, you would have that line at maybe dozens of places and when the time to debug something comes and you see a `Email address is required` in the logs, you can't really tell where it came from.

Sometimes, to make debugging easier, we dump the entire stacktrace in the logs. _But dumping stacktrace in logs causes its own set of problems_:

1. It makes the log become much larger in size.
2. The log becomes very difficult to filter and when displayed, it looks pretty "noisy".
3. They expose a part of architecture of the codebase and that, in wrong hands can be problematic. 
4. Stack traces often show you line numbers but line numbers or file names can change quite often against what you already have in your codebase. So then you need to co-relate the old line numbers with new ones and that doesn't help when you are debugging under pressure.

Logs themselves cannot indicate where they were sent from. A number of logging libraries can tell you the file names and maybe the log "level" but that's it. You can't always pinpoint your log message in code using just that much information. Then again, not all languages (especially compiled ones) would preserve the line numbers of the source code for that to happen.

So what exactly do we need our logs to contain? What's the ideal log message that you can store somewhere?

## What should a Log Message be like?
Summarising the requirements from the above section:

1. Each log message should be **individually identifiable** across the codebase. 
2. The information that helps identify a log message **should not change as the source file updates** - as new code is added (and sometimes old code removed), the error message should still be uniquely identifiable and thus, must not depend on line numbers in the source file.
3. It should **contain some sort of log _level_** - It is one thing to record a user's ID when he signs in your logs and quite another to log the failure to connect to the database! Some log messages are more important than other log messages!
4. Each log message should be able to **carry enough info about error trace without needing a full stack trace dump**.

## Introducing the Log Message Identifier (LMID)
The way to fulfil the requirements we listed above, we need to attach a unique code to each log message. Apart from the requirements above, it should also have the following properties:

1. **Must be easily obtainable** - you can't really depend on a separate central database of unique codes before you actually get a simple log message identifier. It also removes the inhibitions in a developers mind from updating the LMID when he is copying the log with a piece of code from elsewhere!
2. **Must be short** - If you have to dictate someone an error code over a phone, reciting a UUID in all its length and glory is a seriously bad idea. 

## How to obtain a LMID
I use a small script to obtain a new LMID every time I need one. The script looks like this: 

```shell
#!/usr/bin/env zsh
printf "$(([##36]$(date -u +%s) - 1600000000))" | pbcopy
```

> [!info]+ Getting LMIDs from the web!
> Setting up scripts and shortcuts and so on might not be what you love. Don't worry, we have a [dedicated page](https://devta.techrail.in/lmid) to get LMIDs, built and hosted in our other project [[projects/devta/introduction|Devta]] where you get the LMIDs that update every second! That page would also give you LMIDs for different Log Levels supported by [[projects/bark/introduction|Bark]]!

What does this shell script do?  The first line `#!/usr/bin/env zsh` indicates that it is a ZSH script. I mostly code on a macOS. ZSH is always available on macOS. On every linux machine I use for coding also has ZSH on it. It goes without saying that ZSH is required for this script. The second line is where the action happens: 

1. `$(date -u +%s)` takes the current [UNIX Timestamp](https://en.wikipedia.org/wiki/Unix_time) value for UTC.
2. Then we subtract `1600000000` from it. 
3. We then convert the remaining value to [Base36](https://en.wikipedia.org/wiki/Base36) (that's what `[##36]` is doing)
4. Then we print it without any newlines (`printf` does that)
5. And then we send the output to `pbcopy`. This program is always available on macOS and anything you send to it is set in the clipboard. On Linux machines, I typically use [CopyQ](https://hluk.github.io/CopyQ/) - it has a CLI command which allows me to set the value in the clipboard. 

Let's check some properties of the code we get: 
1. **Uniqueness**: This code is basically a converted Unix Timestamp - which changes every second. Unless you obtain two codes in a second and use them (which is practically unlikely), it is always unique. It ensure that even if you are on the move across timezones, this value stays moving ahead at a constant rate - because it is the UTC timestame.
2. **Does not update on file changes**: Once you have pasted it in your log message, it will stay there and irrespective of new changes incoming, it won't change (unless you change it again).
3. **Short**: As of now it produces a 6 character code. It would practically take more than 60 years before it gets 7 charactered. Easy enough to tell someone over a phone.
4. **Reveals absolutely nothing about the code itself**: Even if this logic is exposed to someone else, it never reveals anything about the code structure itself. No line numbers, no file names, no directory structure or the language used to build your program. 
5. **Easily Obtainable**: All you have to do is to bind this script to a shortcut key in your editor and on the press of a button, you would have a new LMID in your clipboard, ready to paste!

So how to use LMIDs in Log Messages?
## Format of a Log Message with LMID
When I write a LMID in my log messages, I format it this way: `<ERR_LVL_>#<LMID> - <LOG_MSG>`.

1. `ERR_LVL` - A single character Indicating Error Level.
	- `P` for Panic
	- `A` for Alert
	- `E` for Error
	- `W` for Warning
	- `N` for Notice
	- `I` for Info
	- `D` for Debug
1. `LMID` - The Log Message ID (obtained using the above mentioned method).
2. ` - ` - to separate log metadata from the actual log message.
3. `LOG_MSG` - The actual log message I want to log.

**Examples (using golang's `fmt.Println` statements)**:

```go
fmt.Println("E#1L0YN0 - User logged in:" + someUser.Id)
fmt.Println("W#1L0YOX - User tried to access admin panel but was denied:" + someUser.Id)
fmt.Println("P#1L0ZA3 - Could not connect to the main database!")
fmt.Println("D#1L1AB7 - Reached this point!")
```

This format keeps my logs easily parsable. This is also the format that [[projects/bark/introduction|bark]] would use so that you can write just plain strings but they could be parsed before they get inserted in the database.

I hope this post helps you write better logs.