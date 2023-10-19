---
draft: true
title: How many severity levels are good enough?
tags:
  - blog
  - vaibhav
  - bark
---
One of the main changes in Go version 1.21 was the inclusion of the `log/slog` package which could perform _structured logging_. The slog library by default uses 4 logging levels which are: Debug, Info, Warn and Error. Now that is usually fine. Typically: 

- _Debug_ log level is used for collecting details which can carry sensitive information and these can be pretty verbose; at least that's how they are meant to be used.
- _Info_ log level is used for things that don't represent any problem but are worth being collected in a log. A good example would be something like a user has logged in, or that a report has been generated.
- _Warn_ (or _warning_)

Bark uses 7 different log levels. 

1. Panic
2. 