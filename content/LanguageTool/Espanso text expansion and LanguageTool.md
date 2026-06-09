---
id: ndffev3ezz
slug: espanso-text-expansion-and-languagetool
title: Espanso text expansion and LanguageTool
created: 2025-02-18 18:03:03
updated: 2025-02-16 19:52:09
tags:
  - languagetool
  - espanso
  - software
---
I'm a sloppy writer, using hyphens in place of em- or en-dashes and three periods in a row instead of an ellipsis. Most of these are picked up by [LanguageTool](https://languagetool.org) and then need to be manually corrected by accepting the alternative suggestion (or ignored, to reappear every time you re-edit the document).

Not a big problem in the overall scheme of things … a *'first world problem'* if ever there was one.

But there's a solution … text expansion. 

Mac OS X has a rather basic version available in `System settings … Keyboard … Text replacement` but there are better alternatives.

[Espanso](https://espanso.org) is the one I use. It's cross-platform, [open source](https://github.com/espanso/espanso), a lot more powerful than I need, and works well.

Configuration uses YAML files and can be global or by application. Text substitutions can include variable expansion, regular expressions or run scripts. There are libraries ([packages](https://hub.espanso.org)) of community-written substitutions *e.g.* emojis 😄, mathematical symbols ∑, or — for the writer testing out page formatting — *[lorem ipsum](https://en.wikipedia.org/wiki/Lorem_ipsum)* generators … in cod-Latin: 

> Curabitur est gravida et libero vitae dictum. Inmensae subtilitatis, obscuris et malesuada fames. Cras mattis iudicium purus sit amet fermentum.

… or English:

> Tell me, pray, what explanation do you put upon their actions? Do you really believe that they charged an armed enemy, or treated their children, their own flesh and blood, so cruelly, without a thought for their own interest or advantage?

It's much easier remembering `:m` generates an em-dash (—) rather than Shift-Option-hyphen (or is it Option-hyphen? No, that's an en-dash which looks like this –), or that `>lorem` can be used to randomly generate some Latin nonsense.

Finally, you can create multiple replacements for a single 'trigger', such as the half-dozen different sign-offs for emails. Typing the trigger (*e.g.* `:sig`) pops up a menu to select from.

*Enjoy!*
