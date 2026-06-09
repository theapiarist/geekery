---
id: epelscc2x9
slug: installing-fasttext
title: 02 Installing fasttext
created: 2025-09-20 13:11:40
updated: 2025-09-20 13:59:02
tags:
  - languagetool
  - software
---
[fasttext](https://fasttext.cc) is *“an open-source, free, lightweight library that allows users to learn text representations and text classifiers”*, and is used by languagetool to help in language identification.

Installation of fasttext using homebrew is either [not possible or deprecated](https://formulae.brew.sh/formula/fasttext), but it's easy to compile from source. 

- create a subdirectory to work in and `cd` into it
- download fasttext `git clone https://github.com/facebookresearch/fastText.git`
- `cd` into the newly created `./fasttext` subdirectory
- type `make` and it will compile to generate a new binary called — unsurprisingly — `fasttext`
- move the binary file to somewhere convenient in your path, such as `/usr/local/bin`(you might need to be sudo for this) and check it can be found by typing `which fasttext` … this will return something like `/usr/local/bin/fasttext`

It's as simple as that. 
