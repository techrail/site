---
draft: true
title: How many severity levels are good enough?
tags:
  - blog
  - vaibhav
  - bark
---
One of the main changes in Go version 1.21 was the inclusion of the `log/slog` package which could perform _structured logging_. The slog library by default uses 4 logging levels which are:  Bark uses 7 different log levels. 

1. Panic
2. 