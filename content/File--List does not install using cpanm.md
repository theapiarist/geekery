---
id: optf2eq6jo
slug: file-list-does-not-install-using-cpanm
title: File::List does not install using cpanm
created: 2025-10-17 20:50:18
updated: 2025-10-17 20:57:34
tags:
  - perl
  - perlbrew
---
If you try to install the perl module File::List using `cpanm` you get an error.
```
m4pro:~ dje$ cpanm File::List
--> Working on File::List
Fetching http://www.cpan.org/authors/id/D/DO/DOPACKI/File-List-0.3.1.tar.gz ... OK
Configuring File-List-0.3.1 ... N/A
! The distribution doesn't have a proper Makefile.PL/Build.PL See /Users/dje/.cpanm/work/1760733436.69054/build.log for details.
```

There *is* a Makefile.PL, but it's buried in a subdirectory of the distribution. 

The solution is simple … [download the module](http://www.cpan.org/authors/id/D/DO/DOPACKI/File-List-0.3.1.tar.gz) and unpack it, copy all files in the resulting `/File/List` subdirectory into `/File`, open a terminal window in the `/File` directory, and then type `cpanm .` at the command prompt.

```
M4pro:File dje$ cpanm .
--> Working on .
Configuring /Users/dje/Downloads/File ... OK
Building and testing File-List-v0.3.1 ... OK
Successfully installed File-List-v0.3.1
1 distribution installed
```
