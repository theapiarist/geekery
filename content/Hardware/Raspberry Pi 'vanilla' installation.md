---
title:
created:
updated:
draft: "true"
tags:
  - raspberrypi
  - linux
  - debian
---
Includes the following:

- Debian fully patched (currently Trixie) full install, but then delete all the directories in `~/` as they're not needed. Might be better in future to use Debian Lite.
- `~/bin` added to $PATH
- [[Use Maestral not Dropbox|maestral]]
- perlbrew and (switched to) perl 5.42.2, `cpanm` and `perlbrew clean` which removes 260 Mb of stuff downloaded during the build process
- rpi-clone
- figlet (and modified `/etc/motd`)
- linuxbrew (this might be superfluous)
- configure aliases in `~/Dropbox/cfg/linux` and modify `~/.bashrc` accordingly

