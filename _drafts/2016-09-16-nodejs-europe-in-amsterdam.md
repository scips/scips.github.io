---
layout: post
categories: it, events
tags: nodejs, nodeeu, nieu
title: NIEU 2016 in Amsterdam
meta:
    subtitle: day two
    synopsys: personal note
    tldr: nodeschool mainly
    image:
    alt:
    credit: Sébastien Barbieri
author:
    name: Sébastien Barbieri
    website: https://scips.github.io/
    twitter: scips
    email: sebastien.barbieri@gmail.com
---

# Node Interactive Day 2

## NodeSchool

*by @jp10k @NodeSchoolAms @NodeSchoolHar*

[NodeSchool](https://github.com/nodeschool/)

In Figures:
* Chapters (by city): 170
* Events: 600+

### Node School Workshops

![Node School Amsterdam Chapter](assets/2016/nieu2016/nodeschool.jpg)

There are self guided lesson modules that would ideally be done in group.
    
Two levels of courses are available: the core module for less experienced users and the elective one that are for more advanced user.

See [NodeSchoo](http://nodeschool.io/). Most module is a simple npm install then running the installed module.

**Workshop have to be install globally** - *maybe a docker to put everything could be nice*

### Today: stream-adventure (-fr)

    npm install -g stream-adventure-fr

## Scalable Web App

*by Eugene Istrati of mitoc group*

See https://deep.mg and mitoc group deep microservices.

Explaining how to build microservice env on AWS https://blog.mitocgroup.com/how-to-create-serverless-environments-on-aws-8485ae039765#.q6pq15gz9

### µService architecture

![Micro service definitions](assets/2016/nieu2016/js_microservice.jpg)

See also [Martin Fowler](http://martinfowler.com/articles/microservices.html) and [Wikipedia](https://en.wikipedia.org/wiki/Microservices)

### Todo MVC

using deepify to deploy accross the whole AWS architecture which is defined by the deep.mg org.

## ES2016 is so 2015

*by @_paulverbeek*

[Slides](http://www.slideshare.net/PaulVerbeek/es6-is-so-2015-meet-es2016-nodejs-interactive-europe)

### TC 39

Ecma International, Technical Committee 39 - ECMAScript

[Stage 0](https://github.com/tc39/proposals/blob/master/stage-0-proposals.md) (ideas) -> Stage 1 (porposals) -> Stage 2 (draft) -> Stage 3 (Candidate) -> Stage 4 (Finished: standard ECMAScript)

### ECMAScript 2016

aka: *ECMA-262 7th edition*

#### Exponentiation op

    x ** y
    Math.pow(x, y);

    let cuber = 3;
    cubed **= 3;

#### includes

    ['a'].includes('a') == true; // similar to indexOf

Why not *contains* instead of *includes* ...  because of mootools, the specification got around mootools, because of the extensive usage.

### ECMAScript 2016??? Final

edition 8th - stage 4 ready stuff: ES2017

link to github tc39 final proposals of master

#### Object.entries

    Object.entries([[],[]]); // for multi dim arrays, objects own properties

#### String padding

    '1'.padStart(3,'0');
    '1'.padEnd(3,'0');

#### getOwnerPropertyDescriptors

     Object.getOwnerPropertyDescriptors(obj); // get everything from the object

with defineProperties you can add property to a target object to merge objects.

to create clone too

#### Async

basically do it with a callback and a timeout. Adding promise help a bit but it's still not easy to read.

    try{
        let value = await doSomethingAsync();
        value += await doSomethingAsync();
    } catch (e) {
        console.log(e.message);
    }

see [ponyfoo.com](https://ponyfoo.com/articles/understanding-javascript-async-await) article

#### Trailing comma

    function foo (
        p1,
        p2,
    ) {}

    foo('aaa','bbb',);

### ECMAScript 2016??? Candidate 

**SIMD.JS**

    var a = SIMD.Float32x4(1, 2, 3, 4);
    var b = SIMD.Float32x4(5, 6, 7, 8);
    var c = SIMD.Float32x4.add(a,b); // Float32x4[6,8,10,12]

Will be used in 3D graphics and video processing, physics simulations or cryptography.

**others**

see http://node.green for more info with node compatibility

Resources: [ponyfoo.com](ponyfoo.com), [2ality.com](2ality.com)

**Note**: 
* **ECMA**: European Computer Manufacturers Association
* **ECMAScript**: ECMA-262
* **TC39**: Ecma Technical Committee 39

## End sessions 

### PM2

Awesome presentation 

http://pm2.keymetrics.io/ is a devops tool (ops mainly) to distribute node apps accross server

### Express

*by Doug Wilson*

Part of Node.js foundation as Incubating Project which enhance quality of the product.

3 layers to express:
* Expressjs: the whole server
* pillarjs: building blocks of express available as module (such as router, send, finalhandler)
* jshttp: low level js http related modules (such as etag, fresh, range-parser, on-finished)

Roadmap: promise in routing, enhance template, query, cookies, new routes syntax, split the project in sub stuff
