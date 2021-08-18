---
title: Operating Systems on my PC 
date: 2019-6-03 19:20:00
categories:
  - pc
  - setup
  - linux 
---

I originally built my first desktop computer in the summer of 2017, just before the [crypto-boom and GPU price spikes](https://storage.googleapis.com/hongalex-static-files/crypto.png) that occurred towards the end of the year. I was pretty happy with the way it turned out, paying about $1100 USD for the following specs:

    1. Zotac GeForce GTX1070 AMP graphics card
    2. 2x8GB of Corsair Vengeance LPX DDR4-3200 RAM
    3. Ryzen 7 1700
    4. WD Black 512GB M.2 NVMe SSD
    5. Gigabyte GA-AB350M motherboard
    6. EVGA SuperNOVA G3 550W Gold fully modular power supply
    7. Corsair 350D Window MicroATX Case

The original purpose was to create a gaming desktop, so obviously I threw Windows 10 on it first. However, seeing it has a ton of computing power, I figured it would be great if I could use it for my development environment as well. Personally, I was never really a fan of Powershell since I was already too used to unix by the time I tried it out. I looked into using the Ubuntu subsystem for Windows for a bit, but never really got in the hang of it either due to weird permissions issues and interfacing between Windows files and subsystem files was confusing. Then, I tried simple installations of Ubuntu and Kali Linux as dual boots on a cheap hard drive that I had, but ended up bricking the installations due to misconfiguring the MBR or something, so I rarely used my PC for anything except Windows after that.

About a year later, I wanted to see if I could get MacOS running. I bought a cheap Crucial MX500 250GB SSD and went to town. Turns out, getting a Hackintosh on a Ryzen kernel is significantly more difficult, but there is a huge community in trying to get MacOS running on Ryzen, and I found a [clear post](https://hackintosher.com/guides/amd-ryzen-hackintosh-guide-installing-macos-high-sierra-10-13/) that got it working in the end. This worked out reasonably well for me, but realized that running MacOS on non-Apple metal creates a whole load of issues. I ran into issues including: Nvidia web drivers failing to keep up to date, no support for Facetime/iMessage, poor audio/bluetooth experience, and random failures when booting up. There was also a resolution issue that I eventually fixed with SwitchResX, but could never get the refresh rate to 144hz for my monitor that supports it. It was pretty cool at first, but I lost interest and didn't boot into my Mac environment for a long time.

This weekend, I remembered that I still had High Sierra on my Hackintosh and wanted to upgrade to Mojave for the fun of it. After looking through the number of issues that people were having, I instead decided to ditch my Hackintosh dreams (until it gets better) for a Debian Stretch installation up and running. [Debian](https://www.debian.org/) is a open-source operating system based on Linux and uses an apt-based package manager. By default, Debian consists entirely only of free software. Google internally uses an in-house version of DebianTesting, so I wanted to try getting a similar experience on my home desktop.

## Bricking Debian

I'm writing this post because within 24 hours of installing Debian, I've bricked my installation. Initially, it was because I was trying to get the latest Nvidia drivers (430.86), while only 390.116 was available through traditional `apt` non-free lists. This was required by [Lutris](https://lutris.net/) as I tried to get games on Linux. Only issue was I failed to completely remove my existing 390.116 version of `nvidia-driver`, which led to a host of issues like `nvidia-installer --uninstall` wanting to remove the conflicting versions everytime I ran `apt install`. After that, I tried removing the default "LibreOffice" apps to free up space, but I think I also removed `lightdm` and maybe even `eth0` because I lost my nice GUI and also the ability to connect to the internet. Needless to say, my installation was done. The following instructions will hopefully servce as a guide to others (and future me) in case this happens again. 

## Steps to setup Debian from fresh install

1. Create USB bootloader with min 8gb USB stick, [Rufus](https://rufus.ie/), and [Debian](https://www.debian.org/distrib/)
2. Boot with your flashed USB stick and select "Graphical Install" with preferred settings:
      * Couple of options here. I personally enjoy [Cinnamon](https://packages.debian.org/search?keywords=cinnamon) for my desktop environment
      * I used an entire 250GB SSD without a partition, but you could partition a larger disk beforehand if you don't have an entire disk to spare.
3. From Debian GRUB menu, do the following to boot with CPU-based graphics. Otherwise you will get a black screen.

      * Press `e` to edit the boot command under the first option.
      * Find the line beginning with `linux` and after `quiet`, add `nomodeset`
      * Press `Ctrl+x` to boot with these settings

4. (Optional) Add your local user to sudoers with:

    `usermod -aG sudo username`
    `su - username`

5. Install some standard packages

    `sudo apt install vim curl git`

6. Add `contrib non-free` to each line in `/etc/apt/sources.list`. This will allow `apt` to find additional packages (like our nvidia-drivers)
7. `sudo apt update && apt upgrade`
8. Install powerline fonts

    `sudo apt install fonts-powerline`

9. Install fish and omf

    `sudo apt install fish`

    `curl -L https://get.oh-my.fish | fish`

    `omf install agnoster`

10. Change default shell

    `chsh -s /usr/bin/fish`

11. Install Albert (spotlight helper for Linux)

    * Navigate to [Albert installer](https://software.opensuse.org/download.html?project=home:manuelschneid3r&package=albert)
    * Add albert to "Startup Applications"
    * Start albert and assign a hotkey. I personally use `Ctrl+Space` and "Numix Rounded" theme
    * Under "Extensions", add all the tools you want to show up
  
12. Reboot machine `sudo reboot`
13. Set up USB 2FA as described in [this article](https://support.yubico.com/support/solutions/articles/15000006449-using-your-u2f-yubikey-with-linux)
14. Download [Chrome](https://chrome.google.com) and [VSCode](https://code.visualstudio.com/) `.deb` files and install them

    `sudo apt install ~/Downloads/google-chrome-stable_current_amd64.deb ./Downloads/code_1....deb`

15. Sync settings with VSCode using [Settings Sync](https://marketplace.visualstudio.com/items?itemName=Shan.code-settings-sync) extension
16. Create ssh key and register with Github
17. Add crypto and weather desklets for Cinnamon

![desklets](https://storage.googleapis.com/hongalex-static-files/desklets.png)

## Wrapping up

I will likely continue to update this post as I find other stuff I should be adding to the setup guide, but this works for me so far. Here are some references I looked at on how to set up [Steam](https://wiki.debian.org/Steam), [Lutris](https://lutris.net/downloads/), and [Go](https://tecadmin.net/install-go-on-debian/).
