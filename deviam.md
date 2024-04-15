---
draft: false
title: Deviam
tags:
  - blog
  - vaibhav
  - golang
date: 2024-04-15
updated: 2024-04-15
aliases:
  - Deviam
---
The word **Deviam** is a play on 3 words: **Debian**, **VM** (stands for Virtual Machine) and **Dev** (stands for Development). Deviam is a Debian Virtual Machine which is preconfigured with a few things. It was created for being used as a common development environment for the [[details|Go Workshop]].

## How to download
It can be downloaded from [here](https://1drv.ms/f/s!ApzGjqB_3CYRklyroD87XO5asT8f?e=gX61U7). The link will take you to a shared OneDrive folder. The Deviam VM is contained inside the _Virtual Machines_ folder. Go to the folder corresponding to your architecture. You will find two sub-folders. One of them contains the full VM as a single file. But it is huge at above 5 GB. If you ever encounter a problem with your network, it would be problematic. Hence, there is a second folder which contains the same contents but split in multiple 7zip files. You would need to have 7zip to unzip the file. 

_Hint_: Try to unzip (using 7zip) the first file. 

**NOTE**: The Apple M1 based VM is still being worked on. It will be uploaded once done.
## How to use the VM?
Deviam is a VMware VM. You would need to download and install VMware Workstation (on Intel based Windows and Linux) or VMware Fusion (on Mac) to use it. A free version is available from VMware's website.

Once you have VMware Workstation or Fusion installed and have extracted the folder containing the files, go to the folder and click on the file ending in `.vmx`. The VM should be launched automatically.

A user named **techrail** is available. The password for the same is `techrail.in`. The user _has sudo privileges_ so you should be fine with it. The root password was not set though.

> [!note]+ Important things to remember
> 1. You cannot run a VM which was not built for your architecture.
> 2. If you are asked if you copied or moved the VM, remember to choose the option that says you copied it.
## What changes does it contain?
The list of changes is here: 

1. Installed `curl` and `zsh` and set zsh as the default shell for the **techrail** user
2. Installed VSCodium (read the note below)
3. Installed the JetBrains Mono Nerd Font ([Nerd Fonts](https://www.nerdfonts.com/) contain icons)
4. Created a new profile in konsole and set this font as the font there. The profile was named deviam and set to default as well. Also, the terminal font in VSCodium was updated to use JetBrains Mono Nerd Font
5. Installed Oh My ZSH and Powerlevel10k theme to spice up the terminal (sane defaults for Powerlevel10k theme)!
6. User's bin directory (`/home/techrail/bin`) was added to PATH.
7. Go and neovim were installed in the user's bin directory and symlinks were created so that they are easily available from the terminal.
8. Installed a few plugins (Packer, Treesitter, Mason etc.) for neovim (check the `/home/techrail/.config/nvim` for details)
9. Go LSP was installed and configured. The LSP is already linked to both neovim and VSCodium.
10. The toolbars for konsole and kate were hidden to make them look a little bit cleaner (these are default programs for terminal and text editor in KDE)
11. The login splash screen and user's login icon was changed to techrail site logo (branding).
12. A total of 3 wallpapers were added to the list of wallpapers and one of them is set as the current wallpaper. The images were created using [Ideogram](https://ideogram.ai). 

> [!success]+ Why VSCodium instead of VSCode?
> It is because VSCode is a Microsoft product and its license specifically disallows redistribution. VSCodium is made on the same open source codebase from which VSCode is built and can be distributed much more freely as it does not contain the changes by Microsoft and technically is not a Microsoft product. It is the same difference between Chromium and Chrome browsers.

## What can I use it for?
Deviam was created for development and minimal changes were done to the default Debian environment. However it is up to you how you use. 

> [!warning]+ Disclaimer
> The VM is provided as is. I bear no responsibility for any changes you do to your system to make it work or any changes done to the VM in any way. Remember that your actions are yours and you are ultimately responsible for its use. I disclaim any liability arising from the use or an attempt to use the virtual machine by you.

That being said, if you have a question regarding its use, you can reach out to me on Discord (in case you have not joined the community, the link is at the bottom of this page) and I will try to help you with it. 

Happy coding!