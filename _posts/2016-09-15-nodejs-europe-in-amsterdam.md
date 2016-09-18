---
layout: post
categories: it, events
tags: nodejs, nodeeu, nieu
title: NIEU 2016 in Amsterdam
meta:
    subtitle: day one
    synopsys: personal note
    tldr: the venue, state of nodejs, µservice, debugging, logging, AI
    image: /assets/2016/nieu2016/venue_01.jpg
    alt: Beurs van Berlage
    credit: Sébastien Barbieri
author:
    name: Sébastien Barbieri
    website: https://scips.github.io/
    twitter: scips
    email: sebastien.barbieri@gmail.com
---

# Venue
Awesome place, old building, great transportation around.
And guess what's here: Banksy expo!

<div class="gallery">
    <span class="cell">
    <img src="/assets/2016/nieu2016/venue_banksy.jpg" alt="Banksy" class="responsive-image" />
    </span>
    <span class="cell">
    <img src="/assets/2016/nieu2016/venue_01.jpg" alt="Beurs van Berlage" class="responsive-image" />
    </span>
</div>

# Node Interactive Day 1

## Opening

*by Mikeal Rogers @mikeal*

1. Fastest growing open source platform in theworld
2. 400 new package every day
3. 2.5 Million user in 2015 -> 5 Million users in 2016
4. Why: Backend, API, Frontend, Mobile, tablets, desktops ... IoT = **The full stack** -> Same tool for any platform (dev, patterns, libs, debugging)
    1. Web
    2. Mobile: Apache Cordova
    3. Desktop; Electron
    4. Dev tools
    5. Cloud: Open Shift, Joyent, Google cloud, AWS, Bluemix (IBM)...
    6. IoT: Jhonny5, on board stuff (Pi, arduino, Intel...)
    7. APIs and µServices

Node is very efficient in single process env which make sens to use it on IoT small, low energy hardware

## Core state of the union

*by James M Snell (IBM) @jasnell*

Today: *85 contributores* with commit access + *1084 individuals* contributors

*2700 commits* since v4.0.0

Going for stability: Improving doc, update tooling, fixing bugs

Canary in the Goldmine: Project that continuously test modules against node major evolution.

Testing: Every non trivial commit runs tests on all platforms ~25

### Versions

New major release every 6 Months.

* Even in April (going to LTS 30 month in October)
* Odd in October

Current LTS: v4.5.0 -> 04/2018

### Roadmap

* Better Web Standards support (including HTTP/2)
* ES6/ES7 Support (Promises, Promise debugging, async await, ES6 Module see @bradleymeck, TC-39)
* Workers
* Native module API: not linked to v8 -> to be independent from v8 updates
* Static error codes (consitency)
* better stream API
* Node.js VM agnostic with ChakraCore
* Improve Embedding (Electron, IoT)
* Internationalization i18n
* Debugging (nodereport,  node --inspect)

## Node Together

*by Ashley Williams @ag_dubs npm manager*

> *Tech has a diversity problem, node has a diversity problem.*

### NodeTogether

    require('all');

Teach node for everyone.

*174 Students* so far

See [Nodetogether](http://www.nodetogether.org/) [@node_together](https://twitter.com/node_together)

The course is mainly using package *motivation* with cats ad the goal is to create an app from scratch. So Student can have a concrete product afterward.

Quotes from the speakers:

>"The current problem in node is the environment... we need to work on that."
>
>"Not being a jerk is not enought, it should be more active welcoming.
It means, listen to people and believe what they say."
>
>"The social problem is a system problem and system problems is what IT is good at fixing."

## Everything we need to know about Node.js Event loop

*by Bert Belder @pisciaureus node.js - libuv - founder of StrongLoop*

Most representation of the event loop on google image are wrong.

In reality, it starts with the program and finish with the process#exit between there are several steps.

### Steps of the NodeJS loop

![node js loop](/assets/2016/nieu2016/js_event_loop.jpg)

*Every box as is own inside loop*

It keeps looping till refs counter reach 0

The ref counter is ++ or -- when system resources are opened and closed (network, disk ...)

The unicorn function depending on the system is relying on epoll_wait() (Linux) or kenvent() (BSD) or GetQueuedCompletionStatusEx() (Windows)

## Javascript Engines

*by @aOviedo*

[Presentation](http://slides.com/a0viedo/demystifying-js-engines#/)

[Doc](http://bit.ly/js-engines)

Comparison of js engines: Spider Monkey, ChakraCore, V8, Javascript Core

## NodeJS from monolith to µService

*by @yunongx*

Netflix comes from a huge Monolithic system and want to move away from it.

In the new system, SemVer is used for API versionning, and there is a middle layer that get all the API requests and redirect them to the appropriate docker running the approriate version.

So one docker per version to isolate everything.

It's easier for the developer too, who only have a VM with some docker on it. One docker = one service/API at a specific version.

## Breaking the monolith

*by @slashdotpeter Peter Marton*

[Slides](https://speakerdeck.com/slashdotpeter/breaking-down-the-monolith-peter-marton-risingstack)

* Split in µServices: 1 DB - 1 Service
* Code by feature
* Do continuous delivery

µService is quite complex to setup for a MVP.

Security concern: [node-http-signature](https://github.com/joyent/node-http-signature)

## Debugging JS

Dumping core in production is necessary when there is an issue but then you have to deal with the dump. The project [PostMortem](https://github.com/nodejs/post-mortem) is there to help dealing with that and provide tools to works with the dump. They try also to have a common dump format to allow dumping and replaying with the best tools.

## Text Mining

*by Philipp Burckland*

Why using JS: 
* it's faster than R or Python (not C and not Python using C libs directly)
* it could be plugged in realtime API running node

Unstructured data is 80% of data and from there with [Latent Dirichet Allocation](https://www.npmjs.com/package/lda)

You can use the figures to have Sentiment analysis and topic modeling for instance.

## From Pterodatcyls and CActus to AI

*by Ivan Seidel Gomes*

Based on the game from google chrome with the dinosaure.

[Let's make the dinosaure learn](https://github.com/ivanseidel/IAMDinosaur)

1. Put sensors on the dinosaur
    1. Distance sensor (distance from the cactus)
    2. Size of the cactus (width)
    3. Speed sensor (speed increase during the game)
2. Gamemanipulator: The sensor are reading image from the running game (RGB) and should find the world constraints
3. Actuators: Send key events

### Neural Network

**IN**: sensor
**OUT**: Key stroke

Code in the middle ... we just need to write code... that doesn't work in machine learning.

Instead it connects input to output via neural network

One Neuron aggregate inputs and provide output a*y + b*z + x

You can add more neurons ... what if we have 100 neurons ... or more

the project use Synaptic library and RobotJS (keypress, read...)

### Genetic Algo

Neurones --> Genetic algorythm (without connection + linear) like DNA

We can make random DNA: the same Genetic Algorythm with random values and run them agains the computer, we put them in life and test them and rank them and remove the bad ones (Natural Selection).

The best one are kept to make something that can be better: joining, crossing over, adding some randomness (mutations) to avoid exact replications.

### When is it ready for production

Never... it can always been improved but are restraint by some other aspect (speed, size, time)

### Pitfalls

* Add logic to prevent the dumb algorythm to raise.
* Robot may really do things to your computer such as moving the mouse away all the time.

## The Cost of Logging

*by @matteocollina*

Based on real life Performance consultancy report. The goal was to reduce latency and number of server.

The more you log, the better, it allows to diagnose the application and easier to debug. But there is a thread of.

Logging a line cost 0.22 ms and most of the time, you not only log, you transport the log (json, socket, write to disk): That's the adapter problem.

Use the pino logger

### pino

Logging 10000 lines -> 250ms
And in extreme mode it bufferise most of the stuff before sending: 10000 lines -> 125ms

How: using epoch instead of date, flatten string [flatstr](https://github.com/davidmarkclements/flatstr), fast safe stringify, quick-format

Transport is held in a separate process, 

### Tools

* [Flamegraph](https://github.com/brendangregg/FlameGraph)
* [AutoCannon HTTP load tester](https://github.com/mcollina/autocannon)

## Instrumentation and Tracing in node.js

*by Thomas Watson @wa7son*

[nodejs/diagnostics](http://github.com/nodejs/diagnostics)

[nodejs/tracing-wg](http://github.com/nodejs/tracing-wg)

Traces are left all along the transaction from the incoming request to the final response.
What if something goes wrong in one part of the program.

To intercept everything the idea is to patch every core operations (setTimeout, ...) that's complex. But there is AsyncHooks.

**console.log()** is getting into an infinite loop with AsyncHooks, use process._rawDebug() instead which is synchronous

Handles are used to transfert things from the JS world to the C/C++ world.

## Pitfalls

Redis doesn't work with this but there is solution ongoing.
