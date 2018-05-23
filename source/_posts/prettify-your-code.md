---
title: Use prettier to format your code, automatically, for all your team
date: 2018-05-22 22:19:33
tags: code
---

As a developer, I highly recommend to use [prettier](https://prettier.io/) in your editor. And today I'd like to go a step further, force and automate code formatting for all your team. No need to discuss the code style any more, don't waste time on the arguments about space or tab, whether or not add a new line. And it's much neat for code diff and review.

It's very easy, only 2 steps.
1. Install *pretty-quick* and *husky*. pretty-quick runs prettier on your changed files and husky gives the hook for precommit.

```sh
yarn add pretty-quick husky --dev
```

2. add this script to your package.json:

```yml
{
  "scripts": {
    "precommit": "pretty-quick --staged"
  }
}
```

Now every time when any team member commit, the changed files will be prettified.

![](https://github.com/azz/pretty-quick/raw/master/img/precommit.gif)
