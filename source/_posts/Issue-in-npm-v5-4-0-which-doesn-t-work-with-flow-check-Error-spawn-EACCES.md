---
title: 'Issue in npm v5.4.0 which doesn''t work with flow check - Error: spawn EACCES'
tags: |-

  - code
  - npm
permalink: issue-in-npm-v5-4-0-which-doesnt-work-with-flow-check-error-spawn-eacces
id: 22
updated: '2017-09-04 12:25:06'
date: 2017-09-04 11:48:29
---

#### Error
4th Sep 2017, Monday. All our node.js builds failed with below error at the step when we run **flow check**

```
> flow check

internal/child_process.js:315
    throw errnoException(err, 'spawn');
    ^
 
Error: spawn EACCES
    at exports._errnoException (util.js:907:11)
    at ChildProcess.spawn (internal/child_process.js:315:11)
    at exports.spawn (child_process.js:365:9)
    at Object.<anonymous> (/opt/app/node_modules/flow-bin/cli.js:17:3)
    at Module._compile (module.js:409:26)
    at Object.Module._extensions..js (module.js:416:10)
    at Module.load (module.js:343:32)
    at Function.Module._load (module.js:300:12)
    at Function.Module.runMain (module.js:441:10)
    at startup (node.js:140:18)
```
#### Cause
First thought it was a flow error of latest version. Downgrade 'flow-bin' to previous version didn't work. It was actually caused by 'spawn' calling files with incorrect permissions. `internal/child_process.js:315 throw errnoException(err, 'spawn');`
NPM v5.4.0 removes executable(+x) permission during installing packages.

#### Solution
fix npm to v5.3.0 works `npm install npm@5.3.0`

---
It's still an open issue in NPM when I wrote this.
https://github.com/npm/npm/issues/18324
