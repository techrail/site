---
draft: true
title: How do we use Logs - storage, speed, access and search patterns
tags:
  - blog
  - vaibhav
---
Logs are of course important. We all know about that; had it been any less than important, there would not be so many logging solutions out there. We created [[projects/bark/introduction|bark]] to solve some problems with logging on a moderate scale. But this article is not about Bark. It is about logs themselves.

Right from the beginning the first use of logs for debugging our software to the time that we use them in production to locate errors and to trace actions of some kind, logs are central to how things work. As we progress in our advancement as a developer by career and experience, the format might change including a few more information than when we started. We start using better libraries and frameworks and start time-stamping our logs and so on. However, through all these, there are a few things about logs that stays constant. This post is about those things that stay constant about how we use logs.

## 