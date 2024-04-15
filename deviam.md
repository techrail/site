---
draft: false
title: Deviam
tags:
  - blog
  - vaibhav
  - golang
date: 2024-04-15
updated: 2024-04-15
---
The word **Deviam** is a play on 3 words: **Debian**, **VM** (stands for Virtual Machine) and **Dev** (stands for Development). Deviam is a Debian Virtual Machine which is preconfigured with a few things. It was created for being used as a common development environment for the [[go-workshop/index|Go Workshop]].

## How to download
It can be downloaded from [here](https://1drv.ms/f/s!ApzGjqB_3CYRklyroD87XO5asT8f?e=gX61U7). The link will take you to a shared OneDrive folder. The Deviam VM is contained inside the _Virtual Machines_ folder. Go to the folder corresponding to your architecture. You will find two sub-folders. One of them contains the full VM as a single file. But it is huge at above 5 GB. If you ever encounter a problem with your network, it would be problematic. Hence, there is a second folder which contains the same contents but split in multiple 7zip files. You would need to have 7zip to unzip the file. 

_Hint_: Try to unzip (using 7zip) the first file. 

**NOTE**: The Apple M1 based VM is still being worked on. It will be uploaded once done.
## How to use the VM?
Deviam is a VMware VM. You would need to download and install VMware Workstation (on Intel based Windows and Linux) or VMware Fusion (on Mac) to use it. A free version is available from VMware's website.

**Note**: You cannot run a VM which was not built for your architecture.

## What changes does it contain?
The list of changes is here: 

1. Installed curl and zsh and set zsh as the default shell for the **techrail** user.
2. Changed the KDE Login Splash Screen.
3. Installed VScodium
4. Installed ZSH and curl
5. Installed the JetBrains Mono NerdFont. 
6. Created a new profile in konsole and set this font as the font there. The profile was named deviam and set to default as well
7. Installed Oh My ZSH
8. Installed Powerlevel10k theme and configured it with sane defaults
9. The user icon of the techrail user was changed. The icon was placed in the pictures folder of the home directory.
10. Neovim was installed 
11. golang was installed 
12. The toolbars for konsole and kate were hidden to make them look a little bit cleaner.
13. neovim was configured with LSP and some other setups done.