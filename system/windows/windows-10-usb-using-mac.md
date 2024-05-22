# How to Make a Windows 10 USB Using Your Mac

[Reference](https://www.freecodecamp.org/news/how-make-a-windows-10-usb-using-your-mac-build-a-bootable-iso-from-your-macs-terminal/)

## Step 1: Download and Mount the Windows 10 ISO file

[Windows10 ISO Download Link](https://www.microsoft.com/en-us/software-download/windows10)

```
hdiutil mount ~/Downloads/Win10_1903_V1_English_x64.iso
```

## Step 2: Format your USB Drive

### Find which disk your USB drive is mounted on

```shell
diskutil list
```

### Format you USB Drive

```shell
diskutil eraseDisk MS-DOS "WIN10" GPT /dev/disk2
```

## Step 3: Copy the Windows 10 ISO over to your USB Drive
The maximum possible size for a file on a FAT32 volume is 4 GB.
One of the files in the Windows 10 ISO – install.wim – is now too large to copy over to a FAT-32 formatted USB drive.

```shell
rsync -vha --progress --exclude=sources/install.wim /Volumes/CCCOMA_X64FRE_EN-US_DV9/* /Volumes/WIN10
brew install wimlib
wimlib-imagex split /Volumes/CCCOMA_X64FRE_EN-US_DV9/sources/install.wim /Volumes/WIN10/sources/install.swm 3800
```

## Step 4: Put your USB into your new PC and start loading Windows

Check your PC's BIOS and change the boot order to boot from your USB drive.

