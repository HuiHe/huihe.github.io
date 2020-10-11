---
title: memory leak in node v12
date: 2020-10-11 14:57:04
tags: node
---

Found memory leak in node v12.14(not only this version), issues have already been fixed in v12.18.2.

Release notes: 2020-06-30, Version 12.18.2
- deps: V8: backport fb26d0bb1835 (Matheus Marchini) #33573
    - Fixes memory leak in PrototypeUsers::Add
- src: use symbol to store AsyncWrap resource (Anna Henningsen) #31745
    - Fixes reported memory leak in #33468

I reproduced this issue locally and here is the heap usage comparison for same code using different node versions.

![](/images/node-memory-leak.png)
