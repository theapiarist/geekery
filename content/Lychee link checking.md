---
id: v1pyj4i133
slug: lychee-link-checking
title: Lychee link checking
created: 2025-02-27 09:04:48
updated: 2025-02-23 20:12:39
tags:
  - ghost
  - perl
---
> [!info] Outdated
> The Ghost API changed and broke my link checking perl script. With a bit of help from Claude I rewrote an improved version. Lychee does all the heavy lifting, but it now sends improved reports by email. I'll update it when I have time.

I've been regularly posting on [*The Apiarist*](https://theapiarist.org/) since about 2014, and it now has ~600 posts and 1.2 million words … and a lot of outgoing links. 

Although I don't fret too much about SEO and Google rankings, I do get frustrated by broken links — and assume my readers do as well — and would prefer that my site has as few of these as possible. At the very least it looks unprofessional and discourages readers from signing up as subscribers or sponsors.

I therefore regularly check the validity of outgoing (and internal) links using [lychee](https://github.com/lycheeverse/lychee). 

I tested a range of link checking scripts and dabbled with writing my own before settling on lychee. After all, why reinvent the wheel?

![[lychee-screenshot.webp]]

In addition, lychee is more than fast enough, and I found it very easy to setup and use. It is available to install *via* [Homebrew](https://brew.sh) on OS X or Linux.

For me, the two stand-out features of lychee are:

- it caches links for a definable period to speed things up rather than rechecking everything every time
- a URL ignore list which can include **regular expressions**

Actually, there's one more — a TOML-format configuration file that makes the command line a manageable length 😄.

There's no point in screening *every* link on *every* page *every* day … and, even if I did, I don't have time to make the necessary edits to my website. I therefore wrote a Perl script to get a list of pages and posts from my Ghost-hosted site (a trivial task using the API), and screen one tenth of them every day. 

```
[https://theapiarist.org/zoom/]
	[404]		https://www.youtube.com/embed/XYbYEywKLzk
```

It returns a dated file of the broken links found together with the error and the originating page and, for completeness, it also emails to prompt me to do something with them 😉. Opening this file in [VSCodium](https://vscodium.com/) gives clickable links to determine whether the target is really unreachable, or is accessible by a human but not the lychee User Agent. If the latter, it gets added to the `.lycheeignore` list.

## Editing legacy HTML pages in Ghost

My Ghost site was imported, as HTML, from a prior WordPress site. 

One of the deficiencies of the Ghost editor is that imported blocks of HTML cannot be searched (CMD-F), although the rendered web page can be. The easiest way I've found to edit these old pages is to select and copy the HTML into [Sublime Text](https://www.sublimetext.com), use its powerful find/replace feature and then paste everything back into Ghost.
