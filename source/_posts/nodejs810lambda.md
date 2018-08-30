---
title: Use async or Promise in AWS lambda handler
date: 2018-08-17 14:56:41
tags: [node, js, lambda]
---

In AWS lambda, before node.js runtime 8.10, although you can use promise across all your code, but in top handler, you must follow the below `callback` pattern. async/await is not supported in handler, even in other functions you must use something like babel to transform your code before deploy.

### Previous callback pattern

```js
const api = require('something');

exports.handler = (event, context, callback) => {
  const getSomthingPromise = api.getSomthing(event);
  getSomthingPromise.then(
    data => {
      callback(null, data);
    },
    err => {
      console.log(err);
      callback(err);
    }
  );
};
```

With the new Node.js 8.10, you can use promise or async/await pattern in handler, just like normal node.js function. And you don't need to pass context and callback parameters, only event.

## Use async/await

#### for sync value without await:
```js
exports.handler = async (event) => {
  return {
    statusCode: 200,
    body: 'ok'
  }
}
```

#### for async value with await:
```js
const api = require('something');

exports.handler = async (event) => {
  const data = await api.getSomthing(event);
  return {
    statusCode: 200,
    body: JSON.stringify({ data })
  };
};
```

## Use Promise

#### for sync value wrap in Promise:
```js
exports.handler = (event) => {
  return Promise.resolve({
    statusCode: 200,
    body: 'ok'
  })
};
```

#### for async:

you can directly return it, but I don't recommend this way
```js
const api = require('something');

exports.handler = (event) => {
  return api.getSomthing(event);
};
```

It's better start from Promise.resolve():
```js
exports.handler = (event) => {
  return Promise.resolve(event)
    .then(api.getSomthing);
};
```

### Summary

To use async or Promise, it's up to your choice. But I'm sure either way is easier than the previous callback pattern. Also to mention again, async/await is actually a syntactic sugar for promise in js.

Ref:
https://aws.amazon.com/blogs/compute/node-js-8-10-runtime-now-available-in-aws-lambda/
