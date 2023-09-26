---
draft: false
title: How to allow a folder to be in git repository without its contents
tags:
  - vaibhav
---
Sometimes we need to create a `tmp` folder in our git repositories to store temporary stuff which we don't really want to sync with the remote. But if you create just a `tmp` directory, it won't get synced unless you also create a file in it and ask git to _track_ it.

There are multiple ways to solve that problem. The one that I personally use is to create a `tmp/.gitignore` file with the following contents: 

```gitignore
*
!.gitignore
```

This tells git to:
1. `*` - ignore anything that is under this directory
2. `!.gitignore` - ...except the `.gitignore` file (the very file in which these lines are written).

It is the simplest solution I could find that can be used for any folder irrespective of its name or place in the source tree!
