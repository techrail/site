---
draft: false
title: What is Bark?
tags:
  - bark
  - logging
  - golang
---
Bark is a small logging server that is supposed to fill in the void between **plaintext log files** and **Terabyte scale,  Application Performance Monitoring and Log Aggregation and analytics solutions for enterprises**. 

It takes very low amount of memory, can accept a lot of requests per second and dumps logs into a [PostgreSQL](http://postgresql.org) database. You can checkout the [bark repository on GitHub](https://github.com/techrail/bark) to learn about what it does _technically_ in detail. 

On this post though, we wanna list out some use cases for Bark, why we built it and how it can help you.

## The idea behind Bark (and its origins)
Bark originates out of (like all software) a specific need that we came across. At work, we had to install our services in a particular environment where our analytics and log aggregation service provider was not allowed to work. Their services were completely off the reach for the environment we were operating in. Now, of course there are software solutions for the analytics apart and most people who work with the kubernetes stack already either use it or at least know about it - Prometheus tied with Grafana is what most people go for and it actually serves well.

But what about logs? Logs are pretty important, if not more important than the analytics. We were doing mostly RDBMS and we did not have the extra bandwidth to study and install a dedicated log aggregator system. It was at this time that we realised the way we used logs, and what our needs were. We wanted a nearly turn-key solution to logging wherein we could easily turn it on to start logging using technologies that we were already familiar with. Something, which probably wasn't oriented towards a large installation that produces 100+ GB of logs but could support our log access patterns well enough and long enough to allow us to implement or integrate a larger, terabyte-scale logging solution with all the bells and whistles.

It was at this time that we realised that there are nearly no solutions that actually fill the gap.

> [!info]- What happened to our problem?
> We were able to setup a logging solution using a pretty well known logging stack within the timeframe. However, none of the backend team felt confident with "what happens when things go down" because we don't have enough expertise with the setup or its components yet.

## How do we access the Logs?
Logs are a little different than your typical relational data. The entire scope of that discussion is beyond the scope of this article, but in general, here are the major differences: 

1. Logs are mostly text.
2. Logs are almost always time-stamped.
3. Logs have a _severety_.
4. Logs are written at a rapid rate but read rarely.
5. Logs are almost never supposed to be accessed "individually", but searched based on one of the attributes, often sorted by timestamp.
6. Log searches are almost always based on "exact" strings and often does not need _variations_. 

Based on the above requirements, the Log requirement is different than typical data.

## So what do we actually want to achieve with Bark?
Coming back to the point - Bark is the response of a need - the need of having something which:

1. Can take in the logs from multiple services at the same time at high speed.
2. Provides you the middle-ground between plaintext log files and terabyte-scale logging systems which are difficult to configure and use.
3. Allows you to structure your logs by severity, service name, session name (e.g. Pod name), error code and maybe more fields.
4. Easy to setup from within a codebase, as a standalone service or inside a kubernetes cluster
5. Uses well-known technologies (PostgreSQL and Golang) circumventing the need to learn a new set of APIs to govern over logs
6. Allows you to filter by any of the attributes listed above.
7. Allows you to set retention policies for your logs your way (e.g. delete all `INFO` level logs from `MyService` that are more than 30 days old) automatically.
8. Is Open Source and well-documented - so you can look under the hood and make changes as you deem fit without having to worry or wait.
9. Has libraries in multiple languages allowing you to use a Bark server to be used from services written in different languages.

While most of these are trust as of our current (version 1) release, there are things we are working on and have open issues for. 

## A little bit more!
Us developers are careless at times, especially when we are under pressure. We tend to copy-paste log messages around from well-working piece of code and then leave them as it is. For that reason, we support the use of a [[logging-errors-properly|LMID or CODE]] in Bark. We highly recommend that you use LMIDs to make your logs more useful. 

We hope you will love using Bark as much as we have loved creating it (or more).

**PS/NOTE**: As we define the Roadmap, add more features and create new issues, we will edit this page.
