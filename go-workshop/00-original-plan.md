---
draft: true
title: Original Plan for the Go Workshop
tags:
  - blog
  - vaibhav
date: 2023-10-04
updated: 2023-10-10
---
## Part 1: Introduction to Go  
  - Why are we learning go?  
      - In other words, why not some other language?  
      - Why and how does go make sense in the backend landscape?  
      - The history of go and how it all fits together  
  - Starting the programming  
      - Installation  
      - Virtual Machine to help you program
      - Hello World  
      - Basic syntax  
      - Variables and Data Types

## Part 2: Jumps, loops and packages  
  - Conditional Statements  
      - if, if-else and if-else ladder  
      - switches, breaks, gotos  
      - for - the only loop  
  - Functions  
      - Declaration and invocation  
      - Named returns, multiple returns  
      - Closures and capture environment  
  - Packages and Modules  
      - Difference between the two  
      - How to create and use a package  
      - How to make a module  
      - The go.mod file  
## Part 3: The built-in stuff  
- Data Structures  
  - Arrays and Slices  
  - Maps  
  - Structs (Structures)  
  - Pointers in Go (and how they are different from C pointers)  
- Interfaces  
  - What they are  
  - How they are useful  
  - Writing good interfaces  
  - How to implement interfaces  

## Part 4: Starting off with our sample program  
- Starting off with our ToDo app  
   - Setting expectations  
   - Creating related data structures  
- Writing a basic UI to our program - as a CLI tool  
   - Interfacing with the CLI  
   - Considering flags  
- Saving the data of ToDo app to a JSON file  
   - Why use JSON  
   - How to read and write to files  
   - How to save everything in JSON  

## Part 5: Error handling  
   - Errors and Exceptions  
       - What are errors in go  
       - How are they different from Exceptions  
       - Error wrapping and propagations  
   - Updating our app to handle and log errors  
       - How to write good error messages  
       - Log Message Identifiers (LMIDs) and how awesome are they!  

## Part 6: Concurrency - the prime feature of Golang  
   - Goroutines theory and introductory examples  
       - What is a routine!?  
       - Intro to cooperative multitasking  
       - Contrast against preemptive multitasking  
       - goroutines - the best of both worlds  
   - Channels and introductory examples  
       - What are channels and their importance  
       - Why are they often linked to goroutines  
       - Buffered vs unbuffered channels  
       - Guarantees provided by a channel  
       - How channels can crash a program if mishandled  
   - Goroutines + Channels (code showcase)  
       - Making a set of goroutines communicate  
       - Showcase building a pipeline of events using goroutines and channels  
       - How to use sync package and waitgroups  

## Part 7: Testing go code  
   - The go unit test framework  
       - Why is testing important  
       - How can you write tests  
   - Debugging go code  
       - The printf vs breakpoints methods of debugging and where they are superior.  
       - Setup your IDE and use the features.  

## Part 8: Updates to the ToDo app  
   - Update the app with goroutines and tests  
       - Update the subpackages with tests  
       - Help achieve high coverage

## Part 9: Databases and API Development  
- Databases with go  
   - Why databases are more important than your code!  
   - The `database/sql` package in Go (the features, the shortcomings and the modularity offered)  
   - SQL vs NoSQL  
   - Concept of a database _driver_  
   - Building your own database type handler
- APIs (theory)
   - Why is it called like that?
   - A Primer on TCP connections and how HTTP is built on top of it
   - Understanding basics of REST
- APIs in code
   - The frontend/consumer perspective
   - The backend/provider perspective
   - Using existing knowledge to build our very first API
   - Anatomy of a request and how it is served
- Web Development
   - Basics of HTML rendering in Go
   - How to use variables to make decisions
   - A walk through the go templating system

## Part 10: Updating our ToDo app  
- Replace JSON file with a SQLite database
   - What is SQLite  
   - Connect with a SQLite DB  
   - Transferring the objects we have to SQLite tables  
   - Write the code  
   - Use interfaces to allow two storage backends  
   - Update the CLI flags to use one or the other backend  
   - Implement APIs so that you can now build a web or mobile based todo app  
   - Update tests
   - Updating the code to work with PostgreSQL database!
 
## Part 11: Garbage collection  
   - Understanding GC in go  
       - Why worry about it? - because OOM can kill your program.  
       - Kubernetes can restart your app but it is _your_ (Not _kubernetes'_) responsibility to take care of your data which might get destroyed or get inconsistent  
       - What does GC do?  
       - The algorithm in brief  
       - Relieving the GC pressure

