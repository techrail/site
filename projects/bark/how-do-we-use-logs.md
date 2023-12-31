---
draft: false
title: The way we use logs
tags:
  - vaibhav
  - bark
  - logging
  - wiki
date: 2023-10-04
updated: 2023-10-10
---
Logs are of course important. We all know about that; had it been any less than important, there would not be so many logging solutions out there. We created [[projects/bark/01-introduction|bark]] to solve some problems with logging on a moderate scale. But this article is not about Bark. It is about logs themselves.

Right from the beginning the first use of logs for debugging our software to the time that we use them in production to locate errors and to trace actions of some kind, logs are central to how things work. As we progress in our advancement as a developer by career and experience, the format might change including a few more information than when we started. We start using better libraries and frameworks and start time-stamping our logs and so on. However, through all these, there are a few things about logs that stays constant. This post is about those things that stay constant about how we use logs.

## Logs are text
Almost all forms of logs are text. Logs can be stored as binary blobs in certain storage formats but they are almost always displayed as text. Logs do not contain images, binary blobs, videos etc. in almost all (if not _all_) cases. Maybe references to such entities, but not those entities themselves. 

You would probably never export or view them as image file, PDFs, videos or anything like that. Hence, logs are almost always in text format. Written as text. Viewed as text.

## Logs are timestamped
Except the times when you are debugging, you almost always want to know _what happened and **when**_. Hence, most of the time, you need your logs to be timestamped. If you look at the logs emitted by some of the popular libraries in various frameworks - Spring, Laravel, Ruby on Rails etc. - they always contain timestamps. It is important because in a situation when you have to run multiple instances of your service, you need to know what was emitted by which instance of the service. They also serve you (sometimes) in determining how long did the previous step take and so on.

When we use plaintext files for storing logs, then the order of the logs themselves tell us the order and that's usually enough. However, as the requirement grows, we often find ourselves needing to know when a certain thing happened.

## Logs have a severity
Not everything that is happening is equally important. For example, it is one thing that a user has entered a wrong password and it is whole another level of important if your application is not able to connect to the cache or the database! So each log has a _severity_ level, indicating how important it is. Most logging libraries use anywhere between 3 to 10 logging levels, sometimes as numbers, sometimes as text, but they are there!

## Logs are written more than they are read
Ask yourself - do you ever really _want_ to go look into logs? No. We sometimes _need_ to, but we almost never want to. We want to send a log on its way and then forget about it. _We only look in there when we need to trace a problem._ Looking into logs is probably no one's hobby or favourite time-pass activity.

## Logs are often not read individually
When we look at logs, we hardly, if ever want to look at a single line of log. We usually look at a portion of a log file (or log stream). Sometimes we look for logs by searching for a specific piece of text in there but we almost never actually check a Log entry's ID and load it again.

In most cases (when we are not debugging), we look for occurrences of log messages containing a particular text or that occurred in a certain time range. Other attributes such as severity, source etc. can also be added in that query. But the statement still remains true - _we do not access logs individually_. We mostly search for them in a large number of log messages.

## Log searches are almost always based on exact strings or phrases
When you search for something on a typical text searching system (e.g. Google or Confluence), you are looking for _related words as well_. For example, if you search Google for the word "butterfly", it would also give you results with the word "butterflies". Or if you search for "person", it might match a web page that contains only the word "people". Such _full-text search (FTS)_ capabilities make these systems amazing and really helpful.

But imagine that you are searching for the line `User is not available` and expect to get a handful of results, your log system decides to be _helpful_ and gives you search results for the line `Users are not available` and there are hundreds of those lines in the result. See the problem?

Logs mostly are searched based on exact terms and all the FTS magic is more of a hindrance for log search system than they are a help.

## Conclusion
Logs are textual data. But the access patterns and requirements for logs is not the same as your normal text data like a blog post or a user profile. There are differences in the way they are created, stored, accessed and searched. When we want to design a logging system, we have to ensure that we are building things the way they would be used. That they contain the necessary features and only those features that make sense in that context.

When we thought of [[projects/bark/01-introduction|bark]], we wanted to ensure that we were building things the way they would be used.
