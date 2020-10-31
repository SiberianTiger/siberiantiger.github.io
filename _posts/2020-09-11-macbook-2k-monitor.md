---
layout: post
title:  "How to Enable HiDPI on a MacBook for a 2K Monitor"
date:   2020-09-11 19:50:00 -0500
author: Siberian Tiger
categories: technical
---

## Preparations

The order does not matter in the following preparation steps.

**Preparation 1:** Install RDM from https://github.com/usr-sse2/RDM/releases/tag/2.3.3. RDM is an application that enables extra resolution options. To allow it to run, you may need to go to `System Preferences -> Security & Privacy`.

**Preparation 2:** Generate a PropertyList file to tell macOS that your monitor deserves the HiDPI mode. Steps:
1. With your MacBook's lid closed, run 
   ```shell
   ioreg -l | grep "DisplayVendorID"
   ``` 
   and 
   ```shell 
   ioreg -l | grep "DisplayProductID"
   ``` 
   in a terminal to know the IDs of your monitor. Note that closing the lid is not necessary as long as you can identify the IDs of your monitor.
2. Convert the decimal IDs to hexadecimals.
3. Creat an blank file named `DisplayProductID-[]` with `[]` replaced by the hexadecimal product ID. 
4. On https://comsysto.github.io/Display-Override-PropertyList-File-Parser-and-Generator-with-HiDPI-Support-For-Scaled-Resolutions/, change `DisplayProductName`, `DisplayProductID` and `DisplayVendorID` to your monitor's and save the content of the PropertyList file to the blank file you just created. If your monitor is 2K, the default `Scale Resolutions` can be left changed.


## Main steps

**Main step 1:** Disable SIP (System Integrity Protection) (reboot required). Steps:
1. Reboot your macOS and press `Command` + `R` to enter the recovery mode.
2. Aftering clicking on your user, choose `Utilities` on the menu bar to open `Terminal`.
3. Run `csrutil disable` and then run `reboot`. After rebooting, you can view the SIP status by running `csrutil status` in a terminal.

**Main step 2:** Copy the created PropertyList file to the needed place by running 
```shell
sudo cp DisplayProductID-[] /System/Library/Displays/Contents/Resources/Overrides/DisplayVendorID-[]/DisplayProductID-[]
``` 
with `[]` replaced by correct hexadecimals. If your macOS is Catalina, you need to run 
```shell 
sudo mount -uw /
```
before you run the `cp` command. Comment: To run `sudo`, your account needs to have a password.

**Main Step 3:** Enable SIP again (reboot required). The steps are the same as in "Disable SIP", except in the last step running `csrutil enable` instead of `csrutil disable`.

**Main Step 4:** Open RDM and select 1920 x 1080 with a flash. The resolutions with a flash are those in the HiDPI modes. 

All set! Congratulations! You can now quit the RDM app and do not need it again until you want to change the resolution.

Note: Some posts mention running in a terminal the following.
```shell
sudo defaults write /Library/Preferences/com.apple.windowserver.plist DisplayResolutionEnabled -bool true
```
Judging from my own experience, it is not necessary to do so. If you happen to run this command and would like to restore to default, simply run in a terminal the following.
```shell
sudo defaults delete /Library/Preferences/com.apple.windowserver.plist DisplayResolutionEnabled
```

## Additional notes

I started to use an external monitor for my MacBook in early February this year. To start with, I chose a *Dell U2415M* monitor ($231 post-tax). The color display was great, the 16:10 aspect ratio being elegant. 
However, switching from MacBook's built-in retina display to a 24-inch HD (1920 x 1200) monitor, I can easily tell a drop in resolution. Actually, the built-in display has 227 DPI while a *Dell U2415M* has 94 DPI.

Consequently, I considered switching to a QHD (2K) or UHD (4K) monitor. I supposed I had to give up on the nonstandard 16:10 aspect ratio but I didn't want a drop in height (compared to Dell U2415M) since I read PDFs often. Within the Dell U series, a 4K monitor costs $500 plus, beyond my budget then.
With these constraints, I decided to buy a 27-inch 2K monitor, both keeping the height and having higher DPI at 109.
Eventually, I got a *Dell U2717D* ($331 post-tax) in mid-March.

The monitor itself was great. However, I immediately noticed another problem that the font size on the screen was too small. In `System Preferences -> Displays`, macOS does offer a variety of scaling choices. However, the scaling is done by adjusting the resolution and thus makes the display much more blurry. As a result, I by no means wanted to enlarge my fonts that way. 

Since I mainly used VS Code, web browsers and Slack on my MacBook, I could alleviate the problem by customizing my font size on these applications. I resolved the blurry PDF display in Preview by switching to Adobe Acrobat Reader.

Note that Windows OS does not have this scaling-resolution tradeoff, and macOS is also free of this tradeoff with a 4K monitor.

For a while, I thought perhaps this problem was because I was using the HDMI connection and maybe using displayport resolves it. Yesterday, however, as I looked at the discussion on this problem on the Internet again, I understood that this problem happened because HiDPI was disabled for 2K monitors on macOS.

Following some posts, I managed to resolve this problem today, and decided to write this blog to both remind myself and spread the information. The main posts that are helpful to me are:
- [How I achieve 125% scaling in my 2K ultrawide monitor in Mac OS Catalina](https://medium.com/@jrmorola/how-i-achieve-125-scaling-in-my-2k-ultrawide-monitor-in-mac-os-catalina-296ebcd19a9f)
- [Force HiDPI Resolutions for Dell U2515H Monitor](https://medium.com/comsystoreply/force-hidpi-resolutions-for-dell-u2515h-monitor-5304e5506214)
- [为macOS 10.15开启 HiDPI，让2K显示器更舒适](https://sspai.com/post/57549)
- [不折腾不舒服 篇一：2K显示器不得不说的尴尬及解决方案，聊聊macOS开启HiDPI](https://post.smzdm.com/p/alpzq4kg/)
- [Macbook外接2K显示器时，如何开启HiDPI?](https://zhuanlan.zhihu.com/p/36913571)
- [开启HiDPI（黑苹果通用。10.12.3通过）](https://www.feng.com/post/11104214)
- [How to turn off System Integrity Protection on your Mac](https://www.imore.com/how-turn-system-integrity-protection-macOS)
- [How to Disable System Integrity Protection (rootless) in Mac OS X](https://osxdaily.com/2015/10/05/disable-rootless-system-integrity-protection-mac-os-x/)
- [macOS Catalina Read-only file system with SIP disabled](https://www.reddit.com/r/macOS/comments/caiue5/macOS_catalina_readonly_file_system_with_sip/)

