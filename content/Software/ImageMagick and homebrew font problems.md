---
tags:
  - homebrew
  - imagemagick
  - fonts
created:
updated:
---
When you install (or upgrade) ImageMagick using [homebrew](https://brew.sh) on Mac OS X it has no fonts listed (you should see those that are available with `magick -list font`) [^1].

[ImageMagick](https://imagemagick.org) used to provide a script to generate a file (called `type.xml`) containing all installed fonts. However, this script appears to have disappeared 😞.

Typically, this file resides with the ImageMagick installation … and so gets overwritten when you do a `homebrew upgrade imagemagick`.

## The solution

1. Create the directory `~/.config/ImageMagick`
2. Use [this perl script](https://musings.fatshark.co.uk/files/34a077e57d0c4bbf/generate_imagemagick_fonts.txt) to create `type.xml` in the created directory. Download the script and change the suffix from 'txt' to 'pl'. Run it from the command line using `perl generate_imagemagick_fonts.pl`. Confirm it has created `~/.config/ImageMagick/type.xml`.
3. Check the installed imagemagick can see the fonts listed using `magick -list font` which should produce something like this:

```
Path: /Users/dje/.config/ImageMagick/type.xml
  Font: Academy-Engraved-LET-Fonts
    family: not defined
    style: Undefined
    stretch: Undefined
    weight: 0
    metrics: not defined
    glyphs: /System/Library/Fonts/Supplemental/Academy Engraved LET Fonts.ttf
    index: 0
  Font: ADTNumeric
    family: not defined
    style: Undefined
    stretch: Undefined
    weight: 0
    metrics: not defined
    glyphs: /System/Library/Fonts/ADTNumeric.ttc
    index: 0
```


[^1]: And note that this command has recently changed from something like `magick -font list`, which now generates the cryptic error `magick: no decode delegate for this image format 'list' @ error/constitute.c/ReadImage/753`

