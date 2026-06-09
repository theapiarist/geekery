---
tags:
  - perlbrew
  - linux
  - debian
  - ionos
  - software
created: 2026-05-12
---
I recently set up an Ionos VPS with Debian Trixie. This is the least expensive VPS I've been able to find (at £1 + VAT per month) other than the 'free' offerings from Google and Oracle.

[Perlbrew](https://perlbrew.pl) would not install, giving errors about being unable to find Cwd.pm (and, once I'd corrected that), Exporter.pm and a slew of other things. 

It turns out that the basic Debian install only includes `perl-base` which [lacks fundamentals](https://packages.debian.org/trixie/perl-base), like those two, and cpan. 

The solution is straightforward (as it always if after you've found the answer). Install the full system perl, using `sudo apt install perl` and then install perlbrew in the usual way.
