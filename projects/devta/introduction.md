---
draft: false
title: Introduction to Devta
tags:
  - blog
  - vaibhav
  - devta
---
One of the most catchy names out there for Indians under the umbrella of **Techrail** is _**Devta**_. The word **Devta** in most Indian languages means _Divine Being_ - beings that are helpful in nature and usually have divine/magical powers.

## What is Devta?
Devta, the project is originally a website which contains a number of helpful utilities for **Dev**elopers, is easy-to-use and is a fully client-side website. It contains utilities such as 

- Base64 encoder/decoder
- Multiple URL Parsers
- JSON to other format converters
- Color Picker
- Hash generator
- SQL Formatter
- API Tester
- JWT Token Parser
- CRON Expression Parser

and a few other utilities. It is modular, written in VueJS (using Vite) and Bootstrap and is a responsive site.

# Why did we build it?
There are other websites that do this. There are apps that also do the same thing offline. Why would anyone build a close of those tools?

Well, there are a few reasons: 

1. There are multiple sites with single tools, but there is no place where all the tools exist at the same place.
2. Most of these sites send data from the browser to their backend.
3. Most of these sites are not open source.

Some of the tools in there can be used for sensitive stuff. For example, JWT tokens, Base 64 Decoders, Database URL Parser etc. can be sensitive items. No one can be sure of what a website is doing with the data that we send it for processing and that can be dangerous for sensitive info.

Hence it is important that whatever we do for processing such data is only done on the user's machine and just in case someone does want to look under the hood to be sure, it is supposed to be Open Source. It is also worth nothing that even if you do not know how to read the source code, you can also go to the Network tab of your browser's Developer Tools and ensure that we are indeed not sending a network request (except for cases when making the network request is the very functionality of the tool e.g. API Tester or DNS data grabber).

## Who is supposed to use this thing?
Devta is a tool for developers. We are mostly into Web Technology and hence our tools are also oriented towards the usecases related to web development. However, we are open to suggestions for new tools and would love your involvement in the project for any bug fixes, enhancements or addition of new tools which is great for any developer!

If you are a Mobile Developer who needs some tools that can be useful, please create an issue and let us know what can be done. Maybe one of the developers loves the idea and helps you solve it!

