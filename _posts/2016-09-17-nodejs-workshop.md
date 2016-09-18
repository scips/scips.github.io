---
layout: post
categories: it, events
tags: nodejs, nodeeu, nieu
title: NIEU 2016 in Amsterdam
meta:
    subtitle: last days
    synopsys: personal note
    tldr: contributing guidelines and general conclusion
    image: /assets/2016/nieu2016/venue_01.jpg
    alt: Beurs van Berlage
    credit: Sébastien Barbieri
author:
    name: Sébastien Barbieri
    website: https://scips.github.io/
    twitter: scips
    email: sebastien.barbieri@gmail.com
---
# Workshop day!

Finally some action!

[Node source compiling, testing](https://addaleax.net/code-and-learn-nieu-2016/)

[Contributing Guideline](https://medium.com/@Trott/node-todo-get-started-contributing-to-node-js-core-fbb4d8015df6#.46ps79lyp)

## Folders

* deps/
* doc/api/
* lib/
* src/
* test/parallel/

## Installing node

    git clone git@github.com:nodejs/node.git
    cd node
    ./configure

## Compile

    make -j4
    
it took me about 20'

## Test it:

    ./node
    process.version

## Build the doc

    make doc
    make doc-only

Output will be in *out/doc/api*

## Make test

run all the test 2'50"

    make -j4 test

most of the time

    make -j4 test-parallel

is sufficient (and take half the time)

## Contributing

[Follow contributing rules](https://github.com/nodejs/node/blob/master/CONTRIBUTING.md)

* fork
* branch
* commit

[Example of contributions](https://github.com/nodejs/node/commit/7f2c9ba1ac343ebdd3d4fbe27757847555bf141d)

# Contributing in general

[openhatch](https://openhatch.org/) thanks @pkafei

# Session about how stream works

To learn about stream, reading the code is a good option (documentation and test are not that perfect).
So here are some entry point to understand concept of the stream.

Different streams:

* [readable stream](npm.im/readablestream): maintained by the stream working group. See _stream_readable.js
* writable stream: See _stream_writable.js

Why use readable stream: because it fixes the stream core

Socket is duplex stream (readable and writable).

Stream are pipes.

## _stream_readable.js

Readable: What is readable state: it's a state object, the stream object create an instance of the stream state to store his state.

Pipe: the pipe use the readable state, use on('data') which write on destination.

Source stream emits data event.
When write returns false it means that we need to slow down (pause) and add a drain event wait.

The drain event is triggered and the writer may write again.

The point of stream is to slow down the speed so the consumer can keep on reading.

Handling errors in piped stream: using [mafintosh](https://github.com/mafintosh/) module [pump](http://npm.im/pump).

# Overall Personal Conclusion of the #NodeInteractive 4 days event

While it's always a good thing to gather community around an event and to meet each other in person, I would have imagined a bit more interactivity in this one. Such has Q&A session, idea gathering (post-it, drawing ...) session.

As Ashley Williams mentioned in her session: effort still seems needed to listen and take into account what the community has to say.

I could rephrase this as: I was glad to contribute to bug fixing but I would have been happier to contribute to the future of nodejs in general. 
It looks like nodejs is well controlled by the one working for big companies all around the project and that's fine because it is where it came from. But if you want free contributors to feel more part of the community some responsability and powers needs to be shared.

However, about the venue and the networking, it really was something enjoyable: a nice place, good food and free time to speak to each others was a great idea. Especially the fact that kernel team members where available and free to speak about anything.

I'm glad for the people I met, I'm glad and proud to have been able to help the nodejs community even a tiny bit. It's always good to give back to the open source world, it makes you feel useful.

Let's try to do it the proper way with a retrospective look:

**to keep**

* NodeSchool / NodeTogether alike interactive hand's on session with mentor in the room
* AI session where really interesting
* Session about how nodejs code works
* Networking time

**to enhance**

* Give time for Q&A
* Add more interaction in the early part (allowing each one to speak the same amount of time: free contributor or not) at least to prepare the collaboration summit with all the idea that will be gethered there



