---
draft: true
title: How much data has dd written?
tags:
  - blog
  - vaibhav
  - linux
  - macOS
---
If you have used Linux for some time and have ever searched for solutions around taking backups of entire disks, you would have come across the tool called `dd` which originally was intended as an abbreviation for _Data Definition_ but is actually also famous as _Disk Destroyer_ because of the ability to destroy data on the disk (if you make a mistake in providing the parameters).

> [!success] I personally refer to dd as the "disk dump" tool because that's what I and many others use it for

In the past, `dd` would not show the details about the amount of data it had written. For that, you would have to go to an activity monitor that can show it. macOS's built-in Activity Monitor app does that. On Linux, you could use one of the various task managers available and on Windows you've had the "Resource Monitor" app for a while too.

However, for most modern versions, you can just add the `status=progress` to the command to see the progress. 