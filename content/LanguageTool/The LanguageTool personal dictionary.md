---
id: zg5ra02uqh
slug: the-languagetool-personal-dictionary
title: The LanguageTool personal dictionary
created: 2025-02-14 02:49:42
updated: 2025-10-14 20:28:33
tags:
  - languagetool
  - obsidian
  - perl
  - software
  - writing
---
>[!warning]
>These instructions are now out of date … I'll provide a revised (and easier) method shortly

My [self-hosted copy of LanguageTool](https://geekery.theapiarist.org/self-hosting-languagetool-on-mac-os-x) works well *except* that the server-side personal dictionary [is not updated](https://forum.languagetool.org/t/personal-dictionary-location-mac-os-x-homebrew/10967/4?) when you select the 'add to personal dictionary' option.

Is there a way to fix this?

I write in [Obsidian](https://obsidian.md), transfer the completed draft to [Ghost](https://ghost.org) and then make the final tweaks using the Ghost editor before posting. I use Vivaldi as my web browser with the [Chrome LanguageTool extension](https://languagetool.org/chrome/).

After a bit of digging around it turns out that there are *three* dictionary locations that are relevant. 

1. The Obsidian LanguageTool plugin, which saves words added to the personal dictionary to `/VAULT/.obsidian/app.json` (where VAULT is the name of the Obsidian vault; note that the subdirectory is hidden).
2. The Chrome LanguageTool extension personal dictionary … I've no idea where this is — perhaps buried in a `.ldb` file? — but its contents can be viewed by clicking on the extension, selecting the 'more advanced settings' gear icon, and then scrolling down the page to the personal dictionary (where you can add/remove words individually, or copy them all to the clipboard).
3. The LanguageTool server-side personal dictionary or — since this is apparently unavailable — the list of custom words which reside in `/opt/homebrew/opt/languagetool/libexec/org/languagetool/resource/en/hunspell/spelling_custom.txt` (at least, they do on my installation; note that these files are language-specific).

Ideally, all three would be synchronised, but anything added to `spelling_custom.txt` (since this is what LanguageTool reads) effectively 'trumps' the other two, so synchronisation can be one-way.

Thirty minutes searching for a way to *automagically* extract the Chrome LanguageTool extension personal dictionary failed to turn up a simple solution, so I decided to bodge things a bit. 

I wrote a [short Perl script](/content/customDict.pl.txt) to extract the words from `app.json`, combining them with any additional words I wanted (*e.g.* those from the Chrome LanguageTool extension which can easily be copied to the clipboard) pasted below `__DATA__` in the script, and the *current* contents of `spelling_custom.txt`, and then regenerates a new `spelling_custom.txt`. Simples.

To make life easier it turns LanguageTool off, backs up the original `spelling_custom.txt` file and, after merging the contents of the three files, removes duplicates, sorts the word list, writes out the new file and finally restarts LanguageTool. 

It also removes all the words from Obsidian's `app.json` to avoid both lists growing unwieldy. The Chrome LanguageTool extension needs to be manually cleared periodically.

The script is run via crontab. However, it can also be run interactively if/when the Chrome Extension personal dictionary is pasted at the end of the file.
