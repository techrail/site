---
draft: true
title: How do we use Logs - storage, speed, access and search patterns
tags:
  - blog
  - vaibhav
---
Logs are of course important. We all know about that; had it been any less than important, there would not be so many logging solutions out there. We created [[projects/bark/introduction|bark]] to solve some problems with logging on a moderate scale. But this article is not about Bark. It is about logs themselves.

Right from the beginning the first use of logs for debugging our software to the time that we use them in production to locate errors and to trace actions of some kind, logs are central to how things work. As we progress in our advancement as a developer by career and experience, the format might change including a few more information than when we started. We start using better libraries and frameworks and start time-stamping our logs and so on. However, through all these, there are a few things about logs that stays constant. This post is about those things that stay constant about how we use logs.

## Logs are text
Almost all forms of logs are text. Logs can be stored as binary blobs in certain storage formats but they are almost always displayed as text. Logs do not contain images, binary blobs, videos etc. in almost all (if not _all_) cases. Maybe references to such entities, but not those entities themselves. 

You would probably never export or view them as image file, PDFs, videos or anything like that. Hence, logs are almost always in text format. Written as text. Viewed as text.

## Logs are timestamped
Except the times when you are debugging, you almost always want to know _what happened and **when**_. Hence, most of the time, you need your logs to be timestamped. If you look at the logs emitted by some of the popular libraries in various frameworks - Spring, Laravel, Ruby on Rails etc. - they always contain timestamps. It is important because in a situation when you have to run multiple instances of your service, you need to know what was emitted by which instance of the service. They also serve you (sometimes) in determining how long did the previous step take. 