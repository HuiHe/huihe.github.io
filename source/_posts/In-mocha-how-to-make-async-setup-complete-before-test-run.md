---
title: 'In mocha, how to make async setup complete before test run?'
tags: [code, mocha, js, async]
permalink: in-mocha-how-to-make-async-request-complete-before-test-run
id: 11
updated: '2016-12-22 23:39:23'
date: 2016-12-22 12:19:07
---

In mocha framework, you can setup/arrange preconditions by using before() beforeEach(), **in** describe and before it.

The sequence of these hooks are: all before() run once, then beforeEach(), tests, afterEach90, and finally after() run once.
 
If you want your asynchronous arrange to be completed before everything else happens, you need to use the done parameter in your before request, and call it in the callback.

Mocha will then wait until done is called to start processing the following blocks.

```
before(function (done) {
   db.collection('user').remove({}, function (res) { done(); }); // It is now guaranteed to finish before 'it' starts.
})

it('test spec', function (done) {
  // execute test
});

after(function() {});
```
**using async/await**
```
before(async () => {
  await db.collection('user').remove({});
);

it('test spec', async () => {
 // execute text
});
```
