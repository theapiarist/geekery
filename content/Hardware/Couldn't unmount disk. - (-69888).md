---
id: agilypirwe
slug: couldnt-unmount-disk
title: "Couldn't unmount disk. : (-69888)"
created: 2025-07-06 16:28:13
updated: 2025-07-15 17:24:27
tags:
  - osx
  - raspberrypi
  - linux
  - hardware
---
I've had this error occasionally pop up on Mac OS X when trying to erase and format an external hard drive (an NVME SSD). It's infuriating; the drive can be read, but unmounting/ejecting it from the desktop fails, as does trying to erase/format it using Disk Utility (or `diskutil` from the command line).

And, each of these things takes *ages*, with the spinning wheel being your only company 😞.

I've suspected a hardware failure in the NVME external case, but usually get the same error on the drive if I swap it into my cute M118 [Fideco external NVME docking station](https://fideco-it.com/products/fideco-usb-3-2-type-c-nvme-sata-external-m-2-ssd-docking-m118).

The solution … reformat the drive on Linux before reinitialising it on Mac OS X.

- Plug the external drive or docking station into a Raspberry Pi (I typically use a RPI Zero; you don't need processing power, you just need access to the command line). Determine the drive name using `lsblk -f`. It'll probably be something like `/dev/sda`.
- Unmount the drive, if it was already mounted `sudo umount /dev/sda1`
- Use `sudo fdisk /dev/sda` (assuming it is /dev/sda, see above) to create a new empty partition table, add a new primary partition, and then write that lot to the drive. `fdisk` is menu-driven, and so the options are as follows: `m` (to see help and read available options), `o` (new empty MBR partition table), `n` (new partition), `p` (primary partition), accept defaults for the start and end locations, `w` (write to the drive).
- if you then run `sudo fdisk -l` you'll get a bunch of text ending with something like:

```
Device     Boot Start       End   Sectors   Size Id Type
/dev/sda1        2048 976773167 976771120 465.8G 83 Linux
```

- Shutdown the Raspberry Pi, recover the disk and plug it into the Mac … it will report that the drive needs to be initiated to use it, and then offer some options. On Apple Silicon I'd normally choose [GUID](https://support.apple.com/en-gb/guide/disk-utility/dsku1c614201/mac) and [APFS](https://support.apple.com/en-gb/guide/disk-utility/dsku19ed921c/22.6/mac/15.0).

What causes the error? No idea. But having wasted the best part of an afternoon on it recently, I thought I'd jot down my solution in the hope it might help others.
