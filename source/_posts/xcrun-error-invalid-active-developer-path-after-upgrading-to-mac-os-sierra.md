---
title: xcrun error invalid active developer path after upgrading to mac os sierra
tags: mac
permalink: xcrun-error-invalid-active-developer-path-after-upgrading-to-mac-os-sierra
id: 12
updated: '2017-01-09 05:52:25'
date: 2017-01-09 05:48:43
---

**Error:**

After upgrading to mac os Sierra, started getting the following error in terminal:

```
xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
```

**How to fix?**

Run the following in terminal:

` xcode-select --install `

**Why?**

The problem is git related. On Mac, git is attached to xcode's command line tools. The above command will download and install xcode developer tools and fix the problem that is one needs to explicity agree to the license agreement.
