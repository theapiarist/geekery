---
id: 5m6oo2zwl1
slug: backing-up-writefreely
title: Backing up writefreely
created: 2025-01-11 18:45:43
updated: 2025-01-12 08:23:30
tags:
  - writefreely
  - restic
  - rclone
  - software
---
I run a couple of writefreely blogs on the cheapest virtual server I could find. It's *so* cheap, that the backup option they provide is almost the same price as the monthly fee for the server.

And, being equally cheap, I wanted an *inexpensive* backup solution ...

First off, credit to [Glyn at underlap](https://underlap.org/backing-up-my-writefreely-instance) for the idea of using [restic](https://restic.net), which was new to me.

Glyn's solution works well, *except* my writefreely installation uses a MySQL database, rather than SQLite. The latter is a single binary file stored alongside the writefreely installation, whereas MySQL stores everything in `/var/lib/mysql/` or similar and needs a bit more care when backing up.

I therefore did the following:

Back up MySQL using `mysqldump` to a plain text file (which can be reimported if needed) using `/usr/bin/mysqldump -u writefreely --databases one two three > /home/user/mysql_backups/DB.sql` 

- you'll need to substitute "one two three" with the names of your databases. 
- I backed up to a subdirectory of my user directory for convenience.
- my writefreely user has the correct privileges to backup the databases.
- `mysqldump` will read a [password from a file](https://stackoverflow.com/questions/9293042/how-to-perform-a-mysqldump-without-a-password-prompt) called `~/.my.cnf`

I then use restic to backup both `/var/www` and `/home/user` directories (and everything below them) with the command  `/usr/bin/restic -r rclone:Dropbox:my-vps/restic-repo -p /home/user/.restic-password backup /var/www /home/user` which incorporates rclone to actually save the backup to a remote Dropbox repository.

- note that restic can also read a password from file, passed to it on the command line

This backs up all my writefreely MySQL databases *and* the complete `/var/www/` directory containing the various templates, static content and scripts.

For convenience, both the `mysqldump` command and the `restic` backup command are in a shell script, called at appropriate times from a cron job, with the output saved to a log file *'just in case'*.

## Pruning unwanted backups

All of which works very well, except the backups will grow bigger and bigger over time, unless they're pruned periodically, keeping those you want and discarding those that are not needed.

Thankfully - because restic repositories are a bit complicated - restic can do this for you, using a combination of `forget` and `--keep-daily` (or whatever your backup strategy is). [See the documentation](https://restic.readthedocs.io/en/stable/060_forget.html) for all the gory details.

For example `restic -r rclone:Dropbox:my-vps/restic-repo forget --keep-daily 7 -p /home/user/.restic-password` will keep daily snapshots for 7 days, discarding anything else.

Again, this is in a shell script called from a cron job.
