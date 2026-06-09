---
id: 4sn90ykh7z
slug: vikunja-docker-and-mac-os-x
title: Vikunja, Docker and Mac OS X
created: 2025-10-12 07:48:17
updated: 2025-10-12 10:53:14
tags:
  - docker
  - vikunja
  - osx
  - software
---
[Vikunja](https://vikunja.io) is an open-sourced, self-hostable, To-Do app. You can use it for project management, planning a book, or writing a shopping list. There's good documentation, a powerful API, and a clean browser-based UI. Although the [commercial version](https://vikunja.io/features/#pricing) is a very reasonable €4 a month, but I wanted to self-host it on a Mac OS X server, using Docker.

Initial attempts failed with permission issues. The [instructions](https://vikunja.io/docs/docker-walkthrough/#ensure-adequate-file-permissions) clearly state that two directories must be created (`./db` and `./files`) and their ownership changed to user id 1000 with `sudo chown 1000 ./db` etc.

That presumably works on Linux where the first user id allocated is 1000, but on Mac OS X the user has an id of 501. 

You can check your user id by typing `id -u` at the command prompt.

So, on Mac OS X (I'm running Tahoe on this server), all you need to do is create the two directories, *without* changing the owner id.

There's one additional change needed in the `docker-compose.yml` file. To avoid unauthorized errors (which first appear when you try to create the first Vikunja account) you [must append the port number](https://github.com/go-vikunja/vikunja/issues/1306) to the `VIKUNJA_SERVICE_PUBLICURL`, as shown below.

This `docker-compose.yml` is the one I use on Mac OS X. The database is sqlite, and it's set up for local network access only.

```
services:
  vikunja:
    image: vikunja/vikunja
    environment:
      VIKUNJA_SERVICE_JWTSECRET: <random password here>
      VIKUNJA_SERVICE_PUBLICURL: http://m1mini.local:3456/
      VIKUNJA_DATABASE_PATH: /db/vikunja.db
    ports:
      - 3456:3456
    volumes:
      - ./files:/app/vikunja/files
      - ./db:/db
    restart: unless-stopped
```
