---
draft: true
title: How many severity levels are good enough?
tags:
  - blog
  - vaibhav
  - bark
---
One of the main changes in Go version 1.21 was the inclusion of the `log/slog` package which could perform _structured logging_. Structured logging refers to attaching some structure to logs and usually that means attaching a _severity level_, a timestamp and maybe other bits of information. 

The most important of these is the timestamp which is pretty easy to implement with a simple wrapper function. Severity levels, often referred to as "log levels" or just "levels" is a little bit more complicated than that.

## Slog Levels
The slog library by default uses 4 logging levels which are: Debug, Info, Warn and Error. Now that is usually fine. Typically: 

- _Debug_ log level is used for collecting details which can carry sensitive information and these can be pretty verbose; at least that's how they are meant to be used. The debug level is more or less separate from the rest because usually this level is used for increasing verbosity of the application during development.
- _Info_ log level is used for things that don't represent any problem but are worth being collected in a log. A good example would be something like a user has logged in, or that a report has been generated.
- _Warn_ (or _warning_) log levels usually indicate something which is not right but can be ignored for now because they don't represent an urgent or fatal problem.
- _Error_ level usually indicate that there was some error. 
### The problem
So far so good. But the problem usually starts near the _Warning_ log level, especially when juxtaposed against the _Error_ log level. The thing is: the meaning and purpose of a log level changes from person to person and from project to project. For example: 

- For a _public website_, a user entering a wrong password can be more like an _Info_ or a _Warning_ level, indicating that a user entered a wrong password - which is a fairly common event. But on a _controlled intranet site_ where the user's browser is known to have a password manager plugin auth autofill features enabled, this can be a more severe problem, especially when repeated. So what should I, as an implementor/develop of such a system call it? Just _warning_, or maybe an error; but that's not an error! Interesting dilemma!
- Not being able to connect to the cache can either be a passable problem which does not cause much of an issue or it can be fatally problematic for a high-traffic website. So when your service discovers that it is not able to connect to the cache, what should this event be logged as? A Warning or an Error?

As you meet more such scenarios, it becomes abundantly evident that just the 4 levels (3, if you keep )
## Bark Log Levels

Bark uses 7 different log levels. 

1. Panic
2. 