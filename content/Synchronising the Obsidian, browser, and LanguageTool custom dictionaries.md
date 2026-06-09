---
id: agzityz13c
title: Synchronising the Obsidian, browser, and LanguageTool custom dictionaries
created: 2025-10-14 20:29:42
updated: 2025-10-14 20:51:18
draft: "true"
---
I use a self-hosted copy of LanguageTool to check my grammar and spelling while writing for [*The Apiarist*](https://theapiarist.org). 

Typically, I'll compose in [Obsidian](https://obsidian.md), upload the draft to the website, and then use the browser-based integral [Ghost](https://ghost.org) editor for the final tweaks, with a web browser plugin for LanguageTool. Both Obsidian and the browser 'use' LanguageTool that I've installed on an (ageing but perfectly satisfactory) Mac Mini M1 on my local network. 

The benefits of using a self-hosted copy of LanguageTool are considerable; privacy, offline writing *etc.* The disadvantage is that, unlike the 

However, the problem is that self-hosted LanguageTool never gets the opportunity to 'learn' the list of specialist words *i.e.* those not found in a standard dictionary (of which there are many, whatever you're writing about *e.g.* scientific names, weirdo spelling of equipment, odd acronyms). This is because:

* The Obsidian LanguageTool plugin **and** the web browser plugin maintain their own *separate* custom words dictionaries.
* The LanguageTool editor does not work with a self-hosted copy of LanguageTool.
