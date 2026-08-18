---
title:
created:
updated:
draft: "false"
tags:
  - maestral
  - dropbox
---
[Maestral](https://maestral.app/) is an open source Dropbox client written in python. Smaller and lighter, and with a good CLI.

**Note** … maestral is [no longer being maintained](https://github.com/samschott/maestral). Search for an alternative?

## Install on OS X

Use #homebrew . It just works!

## Install maestral on Linux

```
$ python3 -m venv maestral-venv
$ source maestral-venv/bin/activate
(maestral-venv)$ python3 -m pip install --upgrade maestral
```

Then create a symbolic link from somewhere in your path to the executable … in my case, this works because `~/bin` is in my $PATH.

`ln -s ~/maestral-venv/bin/maestral ./maestral`

Check it works with 

`maestral --version`

And read the [documentation here](https://maestral.app/docs).

## Sharing links

Note that the CLI works with paths relative to the Dropbox root. So if you're trying to share a file with the absolute path of `/home/user/Dropbox/directory/filename.txt` you would use the command `maestral sharelink create /directory/filename.txt`.

You can list shared links with `maestral sharelink list`.