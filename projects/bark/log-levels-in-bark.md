---
draft: true
title: The 7 levels of log severity
tags:
  - blog
  - vaibhav
  - bark
---
One of the main changes in Go version 1.21 was the inclusion of the `log/slog` package which could perform _structured logging_. Structured logging refers to attaching some structure to logs and usually that means attaching a _severity level_, a timestamp and maybe other bits of information. 

> [!info]+ [[projects/bark/introduction|Bark]] is a structured logging library that can use `log/bark`. 

The most important of these is the timestamp which is pretty easy to implement with a simple wrapper function. Severity levels, often referred to as "log levels" or just "levels" is a little bit more complicated than that. Let's explore the levels in `log/slog`
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

As you meet more such scenarios, it becomes abundantly evident that just the 4 levels (3, if you keep the _Debug_ level separate from the rest) are not enough, especially when we are logging events that might indicate a problem
## Bark Log Levels
Bark uses 7 different log levels (including the _debug_ level). Why 7? Because 10 is way too much and 3 is just not enough. 5 is the sweet spot but wasn't quite enough to adjust some special use cases. So here are the levels, in decreasing order of severity, that we decided to put into Bark and what they mean.

1. **Panic**: This is the error message which is put out right before a program crashes or has to be stopped because of a fatal error.
2. **Alert**: This log level indicates a severe error and is a special log level, separate from the rest in the sense that Bark allows you to write and attach a _hook_ function which can be used to send an alert to a third party service (maybe trigger an email, send a slack or discord message or dispatch a SMS or something similar to alert the developers or site reliability engineers). We will write an article around how to use them.
3. **Error**: This level is for errors which should be fixed ASAP. They are to be used when it is not the end user's fault that triggered it (for example, a user entering a wrong password). 
4. **Warning**: This level is for issues that are not causing any functional problems whatsoever but should be tended to whenever there is time. For example, when the code is using an old method of doing something like an older version of TLS or SSL is being used.
5. **Notice**: When you have a log message which contains some information which contains an actionable info but is not causing any error or problem. For example, when an API expects some optional arguments which were not supplied, you might want to log the event along with the defaults that are being used for those values. 
6. **Debug**: This is the same as any logging library - to be used for times when you need to debug through a flow, usually when developing or testing an application rather than in production.

### Debug by default!
A lot of logging libraries, including some famous ones, do not allow you to print the debug messages by default, especially under their default `production` configuration. While this is a good and mostly a desired effect, it can be a source of trouble 