---
title: Migrate my blog from ghost to hexo
date: 2018-05-20 22:00:00
tags: blog
---

### Why

Last time I updated my blog was about 10 months ago. My blog used to be hosted on my own linux vps. I setup the machine, nginx, nodejs, ghost and the blog. It was fun to put all those things together and enjoy my final product, my blog. But I'm not a real blogger. You see I haven't update it for a long time. And I still have to pay for the vps, domain, and maintain the 'system', not the blog itself.

Github pages is free to host static pages, also coming with a free domain name. And [hexo](https://hexo.io/) is easy to let you build your static blog. BTW, it's on node.js :) It actually only spent me a short time to migrate my blog from my own vps to github.

### How

- backup existing ghost data to json file
- install hexo local
- import ghost data using hexo-migrator-ghost
- test on local
- generate static pages
- deploy blog to github.io
