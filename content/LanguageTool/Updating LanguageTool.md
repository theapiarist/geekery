---
id: uav20q90w8
slug: updating-languagetool
title: 03 Updating LanguageTool
created: 2025-06-27 21:02:34
updated: 2025-09-20 14:01:16
tags:
  - languagetool
  - software
  - writing
---
>[!warning] Warning
>Make sure to read the **Gotcha** at the end of the post *before* starting.

LanguageTool has recently been updated from v6.5 to v6.6 (now 6.8 …). If originally installed using `homebrew` then most things should work when you run `brew upgrade`. However, I found I needed to restart it a couple of times until it would work. In addition, the upgrade creates a new plist file which restricts access to languagetool-server to localhost only.

So, `curl -d "language=en-US" -d "text=did the upgrade work" http://localhost:8081/v2/check` gives the expected half page of JSON verbiage, but there's no access to the server from remote machines on the network (or from elsewhere if you have it on a public-facing machine). This includes from browsers with the languagetool plugin installed, or Clemens Ertle's invaluable [Obsidian community plugin](https://github.com/Clemens-E/obsidian-languagetool-plugin).

The solution is simple, add `<string>--public</string>` to `/opt/homebrew/Cellar/languagetool/6.6` as [[Self-hosting LanguageTool on Mac OS X|described previously]].

Homebrew also now appears to list [fasttext](https://fasttext.cc) as deprecated or disabled (depending on where you look; `brew info fasttext` says it's deprecated, but the [webpage states it's disabled](https://formulae.brew.sh/formula/fasttext)) so we can probably assume it may not be installable via homebrew in the future 😞. However, you can [[Installing fasttext|compile and install fasttext from source easily]].

## Gotcha

Finally, a related #gotcha … updating LanguageTool overwrites the [[The LanguageTool personal dictionary|custom dictionary]]. Make sure you backup a copy of `/opt/homebrew/opt/languagetool/libexec/org/languagetool/resource/en/hunspell/spelling_custom.txt` **before** you update things. 

Don't ask me how I found the last bit out 😞.

I'd recommend using [[Homebrew's 'pin' command]] to control when LanguageTool is updated.
