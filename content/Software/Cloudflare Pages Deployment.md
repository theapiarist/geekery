---
title: Cloudflare Pages deployment
created: 2026-05-19T21:57
updated: 2026-05-19T22:43:39+01:00
tags:
  - network
  - software
  - quartz
aliases:
draft: "false"
---
Having tried Netlify and Github Pages, here is a trial deployment of Quartz/Obsidian for Cloudflare Pages. [Instructions are straightforward](https://quartz.jzhao.xyz/hosting#cloudflare-pages). 

Cloudflare appear to be pushing workers, not pages. If you try and set the Quartz site up as a worker it produces an error of some sort referring to node 20 (or something). 

You can avoid all that by deploying the site properly in the first place … like this …

After selecting the `Create application` button you're presented with the **create a worker** setup. Ignore it and select the link indicated below. After that it's straightforward, and exactly as [described in the Quartz 4 documentation](https://quartz.jzhao.xyz/hosting#cloudflare-pages).

![[CloudflarePages.png]]