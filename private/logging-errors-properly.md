---
draft: false
title: Why we need Log Message Identifiers or LMID
tags:
  - blog
  - vaibhav
aliases:
  - lmid
---
Logging is almost central to software development. Logging is probably more important than coding itself at certain places and times. You need logs to look into the past - to find out what happened - whether it was right or wrong or did someone actually try to steal something from you!? Logs are everywhere. Since the time we software developers learn to code till the point we feel like we have the control over whatever technologies and methodologies we are working on, we use logs to figure out what's happening and what's already happened!

In larger installations and companies, they often have a dedicated _logging infrastructure_ teams which take care of just one aspect - logging. Logging as a discipline of software engineering is pretty vast. When you think about logging on a large scale, you have to think of multiple technologies and disciplines - ingestion, load balancing, databases, search methodologies, storage management and more.

And yet, when you have a problem to debug, oftentimes, we pull our hair in frustration (disclaimer: I do not attribute logging to my balding head 😂). Questions like _who sent this log message_, _from where was it sent_, _when was it sent_, _which user action caused it_, _what are the surrounding logs of that one particular log message in that one user's session_ are very important when you are debugging a nasty bug. It only makes sense to talk about how we can log properly.

## Introduction to the Problem
The biggest problem with logging is created by our own selves - we copy paste code. The intentions are usually noble - we want to copy a well-working code elsewhere to replicate the functionality or to copy it and then modify the behaviour. And while we do that, sometimes (or dare I say most of the times) we leave the log messages in that piece of code untouched. I mean what's the room for innovation in doing a `log.Println("Email address is required")`? But then, if you have copied some sort of code that checks for presence of email in the input, you would have that line at maybe dozens of places and when the time to debug something comes and you see a `Email address is required` in the logs, you can't really tell where it came from.

Sometimes, to make debugging easier, we dump the entire stacktrace in the logs. _But dumping stacktrace in logs causes its own set of problems_:

1. It makes the log become much larger in size.
2. The log becomes very difficult to filter and when displayed, it looks pretty "noisy".
3. They expose a part of architecture of the codebase and that, in wrong hands can be problematic. 
4. Stack traces often show you line numbers but line numbers or file names can change quite often against what you already have in your codebase. So then you start needed to co-relate the old line numbers with new ones and that doesn't help when you are debugging under pressure.

Logs themselves cannot indicate where they were sent from. A number of logging libraries can tell you the file names and maybe the log "level" but that's it. You can't always pinpoint your log message in code using just that much information. Then again, not all languages (especially compiled ones) would preserve the line numbers of the source code for that to happen.

So what exactly do we need our logs to contain? What's the ideal log message that you can store somewhere?

## What should a Log Message be like?
Summarising the requirements from the above section:

1. Each log message should be individually identifiable - Each log message should be identifiable separately across the codebase. 
2. The information that helps identi - as new code is added (and sometimes old code removed), the error message should still be uniquely identifiable.
    
3. Each log message should be able to indicate the cause of it being logged.
    
4. Be able to carry enough info about error trace without needing a full call-stack dump.
