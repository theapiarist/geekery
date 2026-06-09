---
id: bc43lodyye
slug: writefreely-and-images
title: Writefreely and images
created: 2025-01-07 14:38:42
updated: 2025-01-22 13:35:41
tags:
  - writefreely
  - writing
  - rclone
---
When you insert an image in [writefreely](https://writefreely.org) it has to be located *somewhere*.

One solution is to simply link to the image you want elsewhere on the web and hope that it doesn't get moved. This works, but it's not very professional, is likely to fail with images on a CDN, and is certainly suboptimal.

Glyn, on [underlap](https://underlap.org/abstracting-cloud-storage), has another solution where images are hosted on the cloud (*e.g.* Dropbox), and [rclone](https://rclone.org) is then used to mount the remote drive locally from which the files are served. This works well.

Rather than doing this, I've created a `/content/` directory inside the `/writefreely/static/` installation directory. Images are added to this directory using a cron job, run every 15 minutes, that uses `rclone copy` to mirror the content of a Dropbox folder on my desktop machine. Images are therefore hosted 'locally' to the web server, with no additional reverse proxy's to setup *etc.*

`*/15 9-23 * * * /usr/bin/rclone copy Dropbox:rclonedatadir /var/www/vs1/writefreely/static/content/ >/dev/null 2>&1`

This latter solution also necessitates a minor change to the Nginx virtual server configuration file ... simply replace 

`location ~ ^/(css|img|js|fonts)/ {` 

with 

`location ~ ^/(css|img|js|fonts|content)/ {`

When I add images, I can then simply type `![House](/content/house.webp)` ... the URL is short and sweet, the entire site (JS, CSS, images) can all be [backed up](/backing-up-writefreely) together ... all I need to remember is to drop a copy of the image into the local Dropbox folder.
