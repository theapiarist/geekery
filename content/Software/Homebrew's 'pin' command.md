---
id: 9yld5tlswq
slug: homebrews-pin-command
title: Homebrew's 'pin' command
created: 2025-02-05 22:55:36
updated: 2025-02-13 17:37:58
tags:
  - homebrew
  - osx
---
If you don't know what [homebrew](https://brew.sh) is, then this isn't for you ... 

Sometimes it's necessary to 'lock' a particular version or formula, so that it's not *automagically* updated during a routine `brew update`.

Apparently, though I'm not entirely sure why, the `bash` shell is one such formula that [should be updated separately](https://altoplace.com/macos/how-to-configure-the-bash-shell-on-macos/).

`brew pin bash`

Prevents any updates and can be reversed when needed with a simple `brew unpin bash`.

It's worth noting that [[Updating LanguageTool|LanguageTool]] is one that is worth 'pinning'. If this is automatically updated it overwrites the custom dictionary and restricts availability over the network … both are the sort of things I want more control over.
