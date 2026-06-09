---
id: 5s8vn9essd
slug: running-multiple-writefreely-services
title: Running multiple Writefreely services
created: 2025-01-01 12:02:39
updated: 2025-01-12 22:57:08
tags:
  - writefreely
  - linux
  - software
---
I wanted to install and run multiple writefreely services on a single computer. This would leave one executable to upgrade, but I could stop, start and configure the individual blogs separately, as needed. Writefreely has a multi-user option, but I wanted to avoid a 'landing page' and use separate domains for each website, each running as an Nginx virtual server (and, in truth, haven't investigated the multi-user writefreely installation much).

The *simple* way to run multiple services is to install two or more in parallel, using the standard installation instructions but ensuring that each service listens to a separate port, then create additional systemd services, giving each a unique name. 

Simple doesn't mean *correct* ... there are other ways to achieve this.

I did the following:

- Moved the `writefreely` executable to `/usr/local/bin/`.
- Moved the configuration file to somewhere convenient (perhaps under `/etc/writefreely/` is the **proper** place, but I put it in a subdirectory of my home directory for [backup](/backing-up-writefreely) convenience).
- Edit the configuration file so that the four keys ending `_parent_dir` (templates, static, pages and keys) have the fully qualified name of the location in which writefreely was *initially* installed.
- Rename the configuration file so that it's unique; for example, I have one for `geekery` (this site) and another for `talks`. 
- Create a [systemd template unit file](https://fedoramagazine.org/systemd-template-unit-files/) for writefreely. These allow a single service file to control multiple services, based upon the configuration file name passed to the service when it starts. On Debian, this file - named something like `writefreely@.service` - goes in `/etc/systemd/system/`.
- The template unit file contains the following:

```
[Unit]
Description=Writefreely service (%i)
After=syslog.target network.target mysql.service
[Service]
Type=simple
StandardOutput=journal
StandardError=journal
WorkingDirectory=/usr/local/bin
ExecStart=/usr/local/bin/writefreely -c /home/dje/.writefreely/%i
Restart=always
[Install]
WantedBy=multi-user.target
```

Note the following :-
- The WorkingDirectory is that of the writefreely executable
- the ExecStart line contains the fully qualified name of the (moved) writefreely executable, following by the **directory** in which the configuration file is located. 
- The name of the configuration file will be passed to the service on the command line and ends up in %i
- StandardOutput and StandardError are to `journal` as `syslog` has been replaced. This squashes a couple of error messages on startup. Use [journalctl](https://linuxhandbook.com/journalctl-command/) to access, read and follow the logs.

- Enable the service, for example `sudo systemctl enable writefreely@geekery.service` assuming you have a configuration file named `geekery`.
- Start the service, `sudo systemctl start writefreely@geekery.service` and check the status of the service `sudo systemctl status writefreely@geekery.service`.

You should see something like:

![[geekery_status.webp]]

To create additional writefreely sites, repeat the setup, delete the unwanted executable, edit and move the config file making sure it has the correct locations hardcoded within it, and listens to a *different* port, then set up the Nginx virtual server.

Enable and start the service, passing the name of the configuration file to the service, and everything should work smoothly.

I'm sure there are improvements that could be made to this, *e.g.* sharing some of the static files, but I'll leave that as an exercise for the reader.


