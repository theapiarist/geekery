---
title:
created:
updated:
draft: "false"
tags:
  - raspberrypi
  - software
---
Use [Jeff Geerling's](https://rpi-clone.jeffgeerling.com) maintained copy of `rpi-clone`.

```
curl https://raw.githubusercontent.com/geerlingguy/rpi-clone/master/install | sudo bash
```

or

```
git clone https://github.com/geerlingguy/rpi-clone.git
cd rpi-clone
sudo cp rpi-clone rpi-clone-setup /usr/local/sbin
```

[Full instructions and options](https://github.com/geerlingguy/rpi-clone)

## Booting from NVME drive

Copy SD card to NVME with something like `sudo rpi-clone nvme0n1` and then use `sudo raspi-config` (via advanced options) to change the boot order.
