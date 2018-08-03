---
title: FP in js
date: 2018-06-14 06:20:21
tags: code
---

```js
const composeFuncs = (...funcs) => (x) => funcs.reduce((p, c) => p.then(c), Promise.resolve(x));
```
