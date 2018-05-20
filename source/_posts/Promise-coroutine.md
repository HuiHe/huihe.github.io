---
title: Promise.coroutine
tags: |-

  - code
  - node.js
  - coroutine
  - async
permalink: promise-coroutine
id: 21
updated: '2017-07-19 02:45:11'
date: 2017-07-19 02:41:40
---


Promise.coroutine(GeneratorFunction(...arguments) generatorFunction, Object options) -> function

When called, the coroutine function will start an instance of the generator and returns a promise for its final value.

Doing Promise.coroutine is almost like using the C# **async** keyword to mark the function, with yield working as the **await** keyword. Promises are somewhat like Tasks.

>The async/await key words are already available in es2017 and node 8.

Reference  
http://bluebirdjs.com/docs/api/promise.coroutine.html