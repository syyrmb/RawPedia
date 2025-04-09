---
title: Download nightly builds es
contributors:
  - XavAL
  - Benitoite
---

<div class="pagetitle">

Download links for development versions

</div>
<div class="headline">

If you want to try the latest tools and bug fixes and can't wait anymore

</div>

## Intro

Below you can find the latest (or close to it) development version of
RawTherapee, in case you need to follow some tutorial which is using a
development version of the program, or you simply wish to test the
latest additions to the toolbox.

Take into account that those will be **development versions**, and that
mean that you may face instabilities, crashes or incompatibilities with
previous versions. However, they are usually very stable and you may
still be very happy with them. And in case you face some problem, you
can also help the developers [reporting the
misbehaviors](How_to_write_useful_bug_reports.md), so they are
aware of them and will have the opportunity to fix them.

This page won't be updated regularly, so if links get outdated you can
always find the latest builds («versions») in the [RawTherapee nightly
builds
page](https://github.com/Beep6581/RawTherapee/releases/tag/nightly).
When you go there, please ignore any file ending in «**.sha256sum**», or
«**.hash**».

As a more friendly alternative, you can also go to the [RawTherapee
downloads discuss
page](https://discuss.pixls.us/t/direct-download-links-to-the-latest-rawtherapee-development-version/29806),
which will be most likely up to date.

## Linux builds (Appimages)

<big>'''Download link: [latest Linux dev build in Appimage
format](https://github.com/Beep6581/RawTherapee/releases/download/nightly-github-actions/RawTherapee_dev_release.AppImage)</big>

*Next explanation taken from [Appimage
quickstart](https://docs.appimage.org/introduction/quickstart.html#ref-quickstart)
and sligthly edited.*

**How to run an AppImage?**

It’s quite simple to run AppImages: all you have to do is download them,
make them executable and run them. Here you can see how to do it using
the GUI:

- Open your file manager and browse to the folder where you have placed
  the *AppImage* file (make sure you have writing permission in that
  folder)
- Right-click on the *AppImage* and click the *Properties* entry
- Switch to the *Permissions tab*
- Click the the appropriate checkbox depending on the file manager you
  are using:
  - *«Allow executing file as program»* checkbox if you are using a
    *Nautilus-based* file manager (*Files, Nemo, Caja*)
  - *«Is executable»* checkbox if you are using *Dolphin*
  - *«Execute»* drop down list to *«Anyone»* if you are using *PCManFM*
- Close the dialog
- Double-click on the *AppImage* file to run RawTherapee

## Windows builds

<big>'''Download link: [latest Windows dev build for x64 processors (in
a compressed
file)](https://github.com/Beep6581/RawTherapee/releases/download/nightly-github-actions/RawTherapee_dev_win64_release.zip)</big>

Portable applications are those that doesn't need to be installed: you
just place them in a folder where you have write permission, and run the
program double-clicking on it.

<big>'''Download link2: [latest Windows dev build for x64 processors
(executable
file)](https://github.com/Beep6581/RawTherapee/releases/download/nightly-github-actions/RawTherapee_dev_win64_release.exe)</big>

**How to run RawTherapee?**

If you downloaded the compressed, portable file, just uncompress (unzip)
it in a folder where you have write permission. When finished,
double-click *«rawtherapee.exe»*.

If you downloaded the executable file, just run it and wait until the
installation process finishes. Then double-click *«rawtherapee.exe»*.

You may see a warning about an unknown publisher, but you can just
ignore it.

## MacOS builds

You will always have the latest available build in the [packager
website](https://keybase.pub/kd6kxr), among builds for older MacOS
versions, in case the link below is too old or too new for your system.

<big>**Download link 1: [The latest available Universal macOS dev
build](https://kd6kxr.keybase.pub/RawTherapee_macOS_Universal_latest.zip)**</big>

<big>**Download link 2: [The last available intel x86_64 macOS 10.14
build](https://kd6kxr.keybase.pub/RawTherapee_macOS_10.14_x86_64_5.8-3100-g0599a5e96.zip)**</big>

**How to run this macOS RawTherapee?**

You just need to follow a few steps:

- uninstall any previous RawTherapee version from your system, with your
  favorite method
- go to the *Downloads* folder and enter the newly created *RawTherapee
  folder*
- double-click on the new RawTherapee *«.dmg»* file
- in the dialog that will open, click and drag the *RawTherapee* icon
  into the *Applications* icon (all within the dialog window), and wait
  until the program is copied
- go to your *Applications* folder and double-click the *RawTherapee*
  icon

Note: To use the optional rawtherapee-cli command line interface, move
rawtherapee-cli into a folder in your \$PATH (for example
/usr/local/bin) and install the RawTherapee app as above.
