---
draft: true
title: How to allow a folder to be in git repository without its contents
tags:
  - blog
  - vaibhav
---
Sometimes we need to create a `tmp` folder in our git repositories to store temporary stuff which we don't really want to sync with the remote. But if you create just a `tmp` directory, it won't get synced unless you also create a file in it and ask git to _track_ it.

There are multiple ways to solv