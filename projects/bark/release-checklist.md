---
draft: true
title: Release checklist for Bark
tags:
  - bark
  - roadmap
---
1. Docker Container (multi-platform build)
2. Binaries for AMD64, ARM64 (ARM8) for linux. Windows and macOS would be nice too. (Use cross compilation)
3. **Test cases.**
4. **Documentation**
5. Create any needed examples for both client and server in a `examples` directory.
6. Ensure that the constants file has been updated to reflect the version!
7. Make sure that Dockerfile is updated.
8. Write and test the build script and make sure it is working well.
9. Make sure that github hooks and actions are well done.
