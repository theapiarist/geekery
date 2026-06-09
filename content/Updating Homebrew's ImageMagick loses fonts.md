---
id: jqz5e6cv72
slug: updating-homebrews-imagemagick-loses-fonts
title: Updating Homebrew's ImageMagick loses fonts
created: 2026-03-29 10:15:19
updated: 2026-03-29 10:30:11
tags:
  - homebrew
  - imagemagick
  - software
---
A recent update of ImageMagic using Homebrew on Mac OS X led to all the fonts disappearing. Of course, this happened at a time when I was in a rush to produce something and didn't have time to sort out what the proper solution was. *Doesn't it always?*

Here's a quick fix: 

List all the fonts that are currently installed using: `magick list -font`. 

Assuming this list is empty, you need to find out where ImageMagick keeps its configuration files, including the list of fonts it has access to (in a file called `type.xml`). 

The command `identify list configure` outputs the configuration, within which you will find a variable termed `CONFIGURE_PATH` which on my machine was here: `/opt/homebrew/Cellar/imagemagick/7.1.2-18/etc/ImageMagick-7/`. Within that directory you'll find `type.xml`.

- Rename `type.xml` to something else *e.g.* `typeOLD.xml`.

- Download and save [this perl script](https://legacy.imagemagick.org/Usage/scripts/imagick_type_gen) from ImageMagick, and save it somewhere convenient. Make it executable using `chmod +x ./perlscriptname.pl`

- Run the following command to retrieve the names and locations of all system fonts and create a `type.xml` file that ImageMagick can read: `find /System/Library/Fonts /Library/Fonts ~/Library/Fonts -name "*.[ot]tf" | ./perlsscriptname.pl -f - > ./type.xml`

**Note** This command is executed in the directory containing the perl script you downloaded, and generates the `type.xml` output file in the same location.

- Move `type.xml` to the CONFIGURE_PATH directory … which for me meant typeing `mv ./type.xml /opt/homebrew/Cellar/imagemagick/7.1.2-18/etc/ImageMagick-7/type.xml`

List the fonts that ImageMagick can now access using `magick list -font` and order should be restored 😄.
