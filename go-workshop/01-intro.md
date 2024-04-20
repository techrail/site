---
draft: true
title: Introduction - Why Go?
tags:
  - blog
  - vaibhav
date: 2023-10-04
updated: 2023-10-10
---
The aim of this workshop is to equip you with the knowledge of go as a language, its various features and how they make your life easy and to familiarise you with backend programming in general. It's a multi-part series where we will explore various aspects of go and build something useful in the end.

The thing that most people want to do is to jump into the coding. Some of you might be expecting that we will be starting with the famous "Hello World" program. But this is not my intention. The intention is to understand why we wanna do what we are going to do!

## Why go and why not something else?
This course is about backend programming. Before we start, we have to think what backend programming is all about and the best way to think about that is to put it in contrast with other types of programming paradigms and associated requirements.

> [info]+ For the people who love listening and watching
> The contents of this web page are also available online (recorded session):
> <iframe width="560" height="315" src="https://www.youtube.com/embed/AFKqcNIsfuY?si=ZLeVYRcl0V-oA5y1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
### Desktop Apps
Desktop apps run on desktop or laptops. 

- The focus here is mainly on "getting things done". 
- They handle one user at a time, do one thing at a time (usually). 
- They are supposed to be integrated with the OS as much as possible (for example, drag and drop must work flawlessly, windows should look good, the scrolling should be butter smooth and so on).
- Think of Word. They take about a GB of RAM to let you edit text! But people still pay for it and use it because it does what they need it to do!

### Mobile Apps
Same focus as desktop with two significant changes:
- They have a small screen
- The resources are pretty limited (low power, lesser memory, no swap)

### Web Apps (Single Page Applications) or Websites
Same focus as desktop apps with some changes: 
- WebApps are usually not super duper complicated. If they get too complicated, they get slow. And then people start kinda of wanting native apps. 
- Apps that load in the browser are also supposed to be lightweight but since they are written in JavaScript (TypeScript transpiles to JS), they suffer the performance penalty of the language and any overload caused by the browser.
- A lot of **desktop apps** these days are also web apps **wrapped in the Electron** framework which makes them web apps and not true desktop apps because the actual code that is written by the developer is usually website code (HTML, CSS and JS/TS).

### Games
Games are not apps but they are very interesting to look at. Games have a different set of requirements. 
- Games are supposed to work with a lot of graphics rendering systems. 
- They calculate a lot of stuff in parallel
    - The physics engine is calculating movements of all the elements in the games based on what all is visible
    - The graphics engine keeps talking to the graphics hardware and rendering objects on screen
    - Networking engine maintains the connection to the server (in case of multiplayer)
    - Input events system keeps a watch on user inputs
    - Sound engine makes sure you have more realistic sounds based on what is being displayed in the game.

Games are notoriously famous for being the most demanding applications because they engage almost everything that a computer has got to its fullest. I believe nothing pushes the hardware industry as much as games have done. The endless desire to replicate reality and to enthrall our senses to the maximum extent possible.
### Backend and how it is different
Almost every app that we have talked about so far is basically a user-facing app - something that users would work with directly. None of these apps have the problem of dealing with multiple users at the same time because none of them live on a server.

A backend server software has a very different set of requirements than the other types that we have discussed so far. Backend servers are the only type of software, irrespective of what kind of servers they are (messaging, gaming, social media, blogging sites etc.) which need to think about the problem of massive concurrent requests. They are the only software that need to think of the problem of "too much popularity". Let's think of them from the perspective of a service, say gmail.

You use Gmail using multiple interfaces. You can use it using your Web Browser on your Laptop. You can access it using the app using your mobile. You might also use it using an email client such as Apple Mail or Thunderbird. Each of these clients are focused on providing you the best email viewing, organisation and composition features. However, for each instance, the software is focused on only the user - you. However, they all connect to the same backend. They talk to the same email servers.

Assuming that there are about 1 billion users of Gmail (which could be very much a reality) and some people have multiple devices and clients to use the service. If all people get even one email per day and they check the emails regularly then some simple mathematics over conservative assumptions would tell us:

1. For each email being received Gmail has to "accept the email" - Assume 1 operation.
2. The email has to go through filters - some automatic (like categorisation, spam detection, email validity and spoofing detection etc.) and some manual (label setting, auto forwarding rules etc.) - Assume 5 operations 
3. The emails need to be "stored" in whatever database that Gmail uses. - Assume 1 operation
4. If the user uses the Gmail app and conditions are satisfied, it has to dispatch a "push notification". - Assume 1 operation
5. Then, the user opens their Gmail interface (web, SMTP, mobile app, whatever) which causes it to list existing emails - Assume 1 operation
6. The user then opens the email and it is _marked as read_. - Assume 1 operation

If you add these, you can see that there are 10 operations for every single email. Given there are a billion emails that Gmail processes each day, we have 10 billion operations that need to be done in a day. That is over 110,000 operations per second.

No other kind of software has to deal with concurrency requirements on that scale. We took an example of an extremely successful service which the whole world uses so the number are a bit exaggerated. But you can see that the kind of problems faced by a good backend engineer are very different than what a mobile app developer or frontend developer has to worry about.

Look a little deeper and you will see that we also need to understand and optimize databases, caching systems, REST API responses, message passing, notifications (such as Push Notification, SMS etc.) and a lot more for running a good backend service. Everything else that you might be thinking about depends on the backend. If the backend fails, no one would be able to receive or read their emails. It is the center of the show.

## Go was designed to solve "Google's Problem"
So what was Google's problem? You can speculate and guess, maybe!? And I am sure you guys would be right for the most part. Google, even back in 2009 had massive amounts of code. Lots of hardware, millions of lines of code and from a [famous blog post](https://commandcenter.blogspot.com/2012/06/less-is-exponentially-more.html), a lot of time spent compiling that code!

![[go-inspiration.png]]
### Who are the GigaChads behind Go?
That blog post linked there is a legendary blog post. Read it. It is written by one of the core designers of the Go language - 

**Rob Pike 😯** - If you use emojis and love sending cute smileys and red roses on a plastic screen to your girlfriend, it's because of Rob Pike. If you can read in your local language on your mobile phone, it is because of Rob Pike. He is the designer of UTF-8, a very well known encoding scheme for characters that powers the computers to display characters in almost any language. It is also the technology behind Emoji. Rob Pike also worked on an OS named "Plan 9" in the past and has worked with some other legends, such as Ken Thompson in the past.

**Ken Thompson** - In case you did not know is another co-creator of Golang. He used to work with Dennis Ritchie - the famous creator of the C language which practically powers the world today. Almost every operating system is basically written in C. Most hardware related code is written in C. Lots of databases, caches, networking software and firmware are all written in C. Ken himself is the creator the language B, which was the predecessor of C. Ken Thompson however is most known for being one of the major contributors to the UNIX operating system. Linux is Unix like. Which means Ken played a big role in shaping how the servers across the world work today. BSD operating systems are all UNIX derived or UNIX based. macOS is forked from FreeBSD itself. So all your Apple devices - Ken influenced the core of that!

**Robert Griesemer** is the third guy who doesn't have much of a public facing. But if you love churning out Javascript and depend on node libraries which basically compare two integers, it's because of him. He wrote the V8 javascript engine which made JS fast. If anyone remembers the days before and after V8, they would know what magic it was. He also created the JVM which featured the JITing of Java code (Just In Time compilation). If you think your stupid Android phone has got any chance of competing with iPhone's tremendous optimizations, thank Robert - he laid the ground work of JITting and the new JVM that came after Dalvik (ART - Android Run Time) does all the JIT magic to make sure that your apps are stupendously faster.
### Lay back and think being one of those people
These people faced with the problems that they were facing - using a complex, overloaded language that was getting more features than it should which took 40+ minutes to compile on a "Compile Cluster" were inspired to simplify the world. Remember, it's 2007 or 2008. Most of these dudes, these gigachads are old with decades of experience. What are you gonna get?

Think again. OS designer (OS knows how to handle too many things concurrently), language designers (they know how to write a language specification in a weekend), compiler designers (they know how to build a good compiler probably in their sleep), JVM expert focused on concurrency (so garbage collection is no big deal for them) and they are faced with building a language which solves their problems perfectly.

![[go-gigachads.png]]

You are gonna get the simplest, most effective way of expressing your desire to the computer. Remember - programming languages are "languages". Languages are used to express. Programming languages are there to let you express your wishes to the computer so that it can get your work done.

Go, as a result came out as a "simple" language. Simple to learn - they wanted someone new to programming to be able to pickup the language and start writing code. They wanted it to be fast. So they ensured that it is a compiled language, not an interpreted one. And not compiled to Byte Code, but to binary code. They want to make sure it compiles fast, supports concurrency and is garbage collected.

Now, you are entering the world of Google. Google is big. So its problems are big too. They have thousands of computers and these gigachads built a language for them. They designed Go to handle concurrency really well so that the computers don't go underutilized. This is where the concurrency magic people talk about in respect of Golang comes from.

## So what does Golang actually do for you?

- It compiles fast - because the language is simple, the time taken by the lexer, the parser, the compiler is small.
- Generates native code - needs no runtime to be installed
- Runs fast - unlike Java, it uses all the great advancements of the hardware.
- Is garbage collected - but is very intelligent (talk about escape analysis?). With a little bit of understanding, you can actually create something as fast as C.
- Little to no magic - so easy enough to debug (unlike something like Ruby)
- Little verbose but forces you to handle things properly. 
- Comes with unit-testing framework built in the language. 
- Comes with a formatter (gofmt) - so you have the debates of where to put the braces solved for you.
- Cross-platform and cross-compilation - even if you are on one OS like Windows running on an Intel processor, you can still build for Linux running on an ARM processor

One of the things that new programmers often don't care about but experienced programmers know the value of - Maintainability. Go offers something that most programming languages have failed to do - the promise of backward compatibility. Go 1.0 release was done in 2012. The language has evolved a lot over time. New features were added, performance has improved dramatically, existing interfaces have been maintained while new ones have been added over the last 12 years and yet, the code written in 1.0 will compile and work flawlessly with 1.22. I have worked with a project some of whose dependencies were written in 2014. I have added code to it that depends on the latest version. All of that still compiles and runs beautifully. The value of this one property over time is invaluable.

## Go from a career perspective

> [!info]+ This was covered in another YouTube video
> And the video is here (mind you, some content is repeated): 
> <iframe width="560" height="315" src="https://www.youtube.com/embed/tCotbWVhLg8?si=PgFwBVksKsoTF7m7" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

A big reason why people explore a new language or technology is to get a job. As such, when I invited people onto my Discord, one of the first questions were around the lines of "Will I get a job if I know golang?" and like all such questions (replace golang with whatever technology you want) is "you gotta look at the right place".

For example, if you are a networking wizard and you wanna word at a company that primarily makes single-person games, chances are really, really thin and you will find a job there, or a job that satisfies you or helps you grow. Or if you are an Android person who knows Java and Kotlin but wanna word at a company that makes iOS apps, you being welcome there is kinda difficult.

You can be hired only by a person who needs your talent. So the natural question that arises is: Who wants go talent?

### The job market of Go
There are some fantastic projects that have been created in golang. Docker and Kubernetes are the prime examples of how good Go can be. Go is definitely used at Google (they created it) and a lot other places. But if you start looking for jobs in recently created startups, the chances are thin. I think it is more of a societal aftereffect than a technical barrier somewhere.

A lot of startups that get created are done by the people who are just out of college or have been out of college in the recent past (less than 5 years or so). People in college often learn C/C++ and Java. I have also noticed that the college going population thinks that since they can create almost anything using Javascript, learning Javascript will set them up for life.

So people end up learning C, Java, Javascript and Python (because Python is easy to pickup). So most startups are either built in one of those languages (well, except C) or are looking for people who can program in one of those (that way, they get fresh hires who know enough about the stack but won't charge too much for the work). 

> [!warning]- A Note about C
> C is fantastic and before you say a word, remember that your OS is written in it. Some of the fastest, most well written pieces of code that were ever written are written in C. 
> 
> But C is impractical in the world of backend because of the time it takes and carefulness that is required at scale. For that reason, while the web servers are written in C, the web services are often not. And that makes C not that great a career choice for backend programmers.
> 
> **BUT!!** If you know C, and you know the fundamentals of computing (from a C perspective), then any other language becomes so much easier to understand. So please don't undermine C.

But once a company has stood up for some time, they often wanna pivot to something which solves their problems a lot better than their current stack. Go is fantastic in those terms. Go can scale. It has the tools to scale vertically and it has the ecosystem to scale horizontally. 

So a lot of places where you would find Go being used are the _mature startups_. These are the places who started quick with Node or Python (or something else) and now wanna either create new services that are faster or are rewriting pieces of their backend in a better language like Go.

That being said, yet another place where go dominates is blockchain and cryptocurrencies. I don't like crypto a lot but in blockchain, the focus is often on things like a) connecting to a lot of peers b) process data in steps and sequences c) performance

Go delivers on all of them. And maybe it is also some community effect; like how Python got all the initial libraries for AI related work and so the whole AI field developed around Python.

Anyways, Go is growing. A lot of people and places are using Go and the ecosystem is now mature with a lot of libraries, frameworks and people to support you build whatever you need in much lesser time.

I am sure you would love learning go for all the great reasons.