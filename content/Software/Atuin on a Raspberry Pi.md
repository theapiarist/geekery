---
title: Atuin on a Raspberry Pi
created:
updated:
draft: "false"
tags:
  - raspberrypi
  - linux
  - atuin
  - software
  - writing
---
[Atuin](https://github.com/atuinsh/atuin) [installation is straightforward](https://docs.atuin.sh/latest/), but the TUI does not appear when the up arrow is pressed on a Raspberry Pi (if your username is `pi` … and isn't it always?). 

The problem is the username, [as described here](https://github.com/atuinsh/atuin/issues/3472#issuecomment-5109544197), together with a solution.

So, in brief: 

- install atuin using the bash script as described in the documentation
- set up syncing, either by creating a new username/password, or by using the key from *another* installation, then verifying via a web browser (can be done on a headless machine)
- edit `.bashrc` to include `export ATUIN_HISTORY_AUTHOR=pi-user` immediately before the atuin entries (which probably start with `. "$HOME/.atuin/bin/env"`)
- `source .bashrc` and the TUI should work correctly 😄
- finally (optional), edit the atuin configuration file (`nano ~/.config/atuin/config.toml`) to allow [syncing of dotfiles](https://docs.atuin.sh/latest/guide/dotfiles/) … which will work after sourcing `.bashrc` again

There's a useful [atuin cheatsheet](https://atuin.linuz.com) available online, but it omits the alias and variables syncing