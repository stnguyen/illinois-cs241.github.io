---
layout: doc
title: "Kernel Lab"
submissions:
- title: Entire Assignment
  due_date: 12/08/2016 11:59pm
  graded_files:
  - mutex.c
  - mutex.h
  - epoll.c
  - epoll.h
  - Makefile
learning_objectives:
  - Implement a mutex Using C11 Atomics/Signal Handlers
  - Use epoll and your created mutex to download a file
---

## Overview

This seems daunting but you will finally use all of your systems programming knowledge from day 1 to today to fully implement something in the kernel (although we will be doing it in userspace)

This lab is a throwback to know your tools! You are going to have to make the folder and create the files to be graded from scratch!

## mutex

The mutex we are going to implement is going to need to use the following function call

```

int atomic_compare_exchange_weak_explicit(int* addr, int* expected, int value, memory_order succ, memory_order fail)

```

What this does is atomically takes the the value at `addr` and compares it to the value at `expected`. If those two are equal then it will stick the `value` into the `addr`. If those to values are not equal what was at `addr` is written into `value` for the memory order commands we suggest you use `memory_order_relaxed`.

What you want to do is be able to create a lock using a struct that may just contain an integer for the lock and use atomic operations to lock and unlock it. Here is what your mutex should do for posix specification.

- lock mutex should only let other threads continue
- all other threads should be blocked
- unlocking a mutex should only be allowed by the owner of the mutex, think of how you can use the atomic instruction above to do this.

We want you to implement normal mutexes, don't worry about recursive mutexes and the like. For an explanation of Mutexes check the video at the bottom.

**PLEASE GO TO THE BOTTOM AND WATCH THE VIDEO BEFORE ATTEMPTING TO IMPLEMENT**

## Epoll Downloader

We are going to pass your program a list of urls, and you should download those using a worker pool of 4 threads. You can use whatever programming model you want so long as the threads are grabbing a url using networking calls to get a connected file descriptor and triggering a read with epoll. Check the wikibook for an example of epoll.

The calls to epoll is

```
int epoll_ctl(int epfd, int op, int fd, struct epoll_event *event);

int epoll_wait(int epfd, struct epoll_event *events,
                      int maxevents, int timeout);

```

The parameters are a lot to dig through so bear with us.

* `int epfd` - A file descriptor to the epoll object you created
* `int op` - One of the operations described in the man page
* `int fd` - The file descriptor to keep track of
* `struct epoll_event *event` - A struct full of options you will also need to read the man page

The timeout and max events in wait are after you add the file descriptor to the epoll object (and depending on what mode you are waiting on).

There will be a demo in Lab showing you some sample code and we will deploy a simple downloader to get you familiarized.

This function call is pretty heavy on the learning curve but once you have gotten all the parameters out of the way, writing the downloader is as simple as a few reads and writes among all the threads. Think about what you need to keep thread safe among all the threads, which files are downloaded/in the process?

In the end, we should be able to compile your epoll lab using your Makefile. We should be able to run your downloader as `./epoll_downloader <url1> [url, ...]`

We will be testing a speedup of many different small files (that is where the concurrent part of the downloader shines).

## Makefile

You have been using `make` for a while, write a makefile yourself!

All you will have to do is when we type `make` it should produce your `epoll_downloader` executable.

## Testing

**Testing is ungraded, but highly recommended**

You are going to have to write your own tests for mutex.h.

For epoll downloader if you run `./epoll_downloader <url>` it should grab any valid url. For concurrent uses, try `./epoll_downloader <big_url1> <big_url2>`

## Files to be graded

*   `mutex.c`
*	`mutex.h`
*	`epoll.c`
*	`epoll.h`
*	`Makefile`

**Anything not specified in these docs is considered undefined behavior, and we will not test it.**


## Video Resources

# [Mutex Implementation in 4 Minutes](https://www.youtube.com/watch?v=dQw4w9WgXcQ)

## Just kidding!

There isn't really a lab.  Lab section will be spent as Office Hours, where you can engage with your fellow students and TAs about material in the course.

The grade for this lab will be the final review packet submission, for which you already have a piazza post about.

Thanks for a great semester. We hope you enjoyed the class and maybe learned a thing or two, and we wish you luck on the final!

You can **ignore** the submission instructions below.