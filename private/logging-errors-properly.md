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