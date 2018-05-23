---
title: Use CODEOWNERS to receive code review automatically
tags: [code, github]
permalink: use-codeowners-to-receive-code-review-automatically
id: 18
updated: '2017-07-13 03:07:45'
date: 2017-07-13 03:04:43
---

In my current project, we are not allowed to commit to master directly. Everyone has to create a pull request first, pass all the automation checks, then a code review is also required. Everytime, the pull request creator has to select all the team members one by one to add them into the reviewers list one the right panel on github page. It's a bit annoying and time consuming.

Using __CODEOWNERS__ file, code owners are automatically requested for code review when pull request created.

Just create a new file called CODEOWNERS in the root or .github/ folder.

Example file:
```
# This is a comment.
# Each line is a file pattern followed by one or more owners.

# These owners will be the default owners for everything in the repo.
# Unless a later match takes precedence, @global-owner1 and @global-owner2
# will be requested for review when someone opens a pull request.
*       @global-owner1 @global-owner2

# Order is important; the last matching pattern takes the most precedence.
# When someone opens a pull request that only modifies JS files, only @js-owner
# and not the global owner(s) will be requested for a review.
*.js    @js-owner

# You can also use email addresses if you prefer. They'll be used to look up
# users just like we do for commit author emails.
docs/*  docs@example.com
```

---
_Reference_
https://help.github.com/articles/about-codeowners/
