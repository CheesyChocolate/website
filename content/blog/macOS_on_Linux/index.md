+++
title = "macOS on Linux"
date = 2025-01-24
updated = 2025-01-25
description = "How to run macOS on Linux, and how to optimize and configure macOS post-installation."

[taxonomies]
tags = ["macOS",
        "Linux"]
+++

# Installations

There are docker, script, and many other ways to run macOS on Linux. But I
found the [quickemu](https://github.com/quickemu-project/quickemu) to be the
easiest and fastest way to run macOS on Linux.

The latest version of macOS that I could get to work is `ventura`. To get the
`ventura` version, you can use the following command:

```bash
quickget macos ventura
```

Then just run the `.conf` file created by the above command:

```bash
quickemu --vm macos-ventura.conf
```

Choose the `macOS Base System` ...

Choose the `Disk Utility` ...

Find the large disk (size > 100 GB) and erase it. Choose `APFS` if you want to
use the disk for macOS only inside the VM. Choose `macOS Extended (Journaled)`
if you want compatibility with Linux, and you want to share the disk between
operating systems. Then go back to the main menu.

Choose `Reinstall macOS` ...

Choose the disk you just erased ...

On boot, choose the disk name you just installed macOS on ...

# Post-Installation

## Optimize macOS

_Source: [osx-optimizer](https://github.com/sickcodes/osx-optimizer)_

```bash
defaults write com.apple.loginwindow autoLoginUser -bool true
mdutil -i off -a
nvram boot-args="serverperfmode=1 $(nvram boot-args 2>/dev/null | cut -f 2-)"
defaults write /Library/Preferences/com.apple.loginwindow DesktopPicture ""
defaults write com.apple.Accessibility DifferentiateWithoutColor -int 1
defaults write com.apple.Accessibility ReduceMotionEnabled -int 1
defaults write com.apple.universalaccess reduceMotion -int 1
defaults write com.apple.universalaccess reduceTransparency -int 1
defaults write /Library/Preferences/com.apple.SoftwareUpdate AutomaticDownload -bool false
defaults write com.apple.SoftwareUpdate AutomaticCheckEnabled -bool false
defaults write com.apple.commerce AutoUpdate -bool false
defaults write com.apple.commerce AutoUpdateRestartRequired -bool false
defaults write com.apple.SoftwareUpdate ConfigDataInstall -int 0
defaults write com.apple.SoftwareUpdate CriticalUpdateInstall -int 0
defaults write com.apple.SoftwareUpdate ScheduleFrequency -int 0
defaults write com.apple.SoftwareUpdate AutomaticDownload -int 0
defaults write com.apple.loginwindow DisableScreenLock -bool true
defaults write com.apple.loginwindow TALLogoutSavesState -bool false
```

## Change resolution

> WARNING: Never change the resolution using macOS system settings. It breaks
> in my experience. In my case, I was using the `Display:  SDL, VGA, GL (on),
> VirGL (off) @ (1280 x 800)` option in QEMU. And after changing the
> resolution, the bottom 70% of the screen was black.

_Source: [macOS-Simple-KVM](https://github.com/foxlet/macOS-Simple-KVM/blob/master/docs/guide-screen-resolution.md)_

NOTE: Skip step 1 to 3 if the resolutions already exist in BIOS.

1. In the macOS Finder, look for **EFI** in the left bar under **Volumes**. If
   it isn't visible you will have to mount it:
    - Open the macOS Terminal and type `diskutil list` and look for the
    disk/partition location of the EFI. (There may be more than one.)
    - Type `sudo diskutil mount diskYsZ`, using the disk/partition location
    name where you see EFI. Most likely it will be `disk1s1`. The one next to
    `Linux Filesystem` not `Apple_APFS`.
    - The **EFI** partition will appear in the left Finder bar under
    **Volumes**.
    - If you don't see anything in that volume after browsing to it, try the
    other ones that you found in `diskutil`.
2. In the **EFI** volume, go into the `OC` directory and open the
   `config.plist` file in the macOS text editor.
3. There should be a section of the file that looks like this:

```````````````````
<key>ScreenResolution</key>
<string>1280x720</string>
```````````````````

 - Edit that to your preferred screen resolution.
 - Some odd/intermediate resolutions like 1366×768 may not work well. Try to
 stick to more common 16:9, 16:10, and 4:3 form factors.

4. Shut down the VM, relaunch it.
    - Press `Escape` key as soon as the window comes up.
    - In the interface that comes up, select `Device Manager`->`OVMF Platform
    Configuration`->`Change Preferred` and select the correct resolution.
    - Press `F10` to save the changes.
    - Press `Escape` multiple times to come back to main menu, and then select
    `Continue` on it.
