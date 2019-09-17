---
title: "Multithreading"
last_modified_at: 2019-09-17T11:20:02+12:00
categories:
  - Teaching
tags:
  - Threading
  - Multithreading
  - Operating Systems
toc: true
toc_label: "Contents"
toc_icon: "cog"
---

So, you’re confused on what 'Multithreading' is. Don’t worry, most people are to some extent. Multithreading is likely one of those things you probably still won't fully comprehend no matter how competent you are (partially because it's a difficult topic, but also because quite a lot of it is sort of undefined in a way, but more on that later).

## Types of multithreading
Threads exist in multiple ways. There are at least four different types of threads (depending on who you ask, and how you define 'thread'):
 - Kernel/System threads
 - Userspace/Green threads
 - Fibers
 - Coroutines

For now, we will ignore fibers because as far as I'm aware Java doesn't use them. We'll also ignore coroutines (as, even though they do exist in Java, I don't know much about them nor do I think you're using them).

Java does do something slightly weird here, so terminology may be a little hazy.

## Userspace/Green threads
These types of threads are generally to kernel threads what kernel threads are to processes (more on this later). Java may have used these at some point, but most (if not all) threading you do in java will use the superior (in many ways, less so in some others) kernel threads. What I mean by this is that Java does provide you with 'user' threads, but these are backed by kernel threads by the JVM (of which your program will only run one of, with the idea that you can then share resources such as classes, objects, etc inside the threads).

## Kernel/System threads
Kernel threads, or system threads, are threads that the Operating System is aware of. Each kernel thread will run in a singular process, of which each process may have many different kernel threads.

Any kernel threads that share a process will inherit the resources used by that process, and indeed share each of those resources. This is essentially how the JVM works in regards to threading -- it provides you user threads, all backed by kernel threads.

## Multithreading in Java
