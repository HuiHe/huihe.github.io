---
title: Node.js 8.10 available in AWS lambda
date: 2018-08-17 14:56:41
tags: [node, js, lambda]
---

In AWS lambda, using node.js before runtime 8.10, although you can use promise across all your code, but in top handler, you must follow this `callback` pattern. async/await is not supported in handler, even in other functions you must use something like babel to transform your code before deploy.

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

- async/await

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

- promise

```js
const api = require('something');

exports.handler = (event) => {
  return new Promise((resolve, reject) => {
    api.getSomthing(event)
    .then((data) => {
        resolve data;
    })
    .catch(reject);
  });
};
```

or

```js
exports.handler = (event) => {
  return Promise.resolve(event)
    .then(api.getSomthing);
};
```

- for sync value, you need to wrap it in promise:

```js
exports.handler = (event) => {
  return Promise.resolve({
    statusCode: 200,
    body: 'ok'
  })
};
```

Ref:
https://aws.amazon.com/blogs/compute/node-js-8-10-runtime-now-available-in-aws-lambda/
