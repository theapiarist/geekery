---
id: n9gey1y64u
slug: getting-and-setting-the-mac-os-x-hostname
title: Getting and setting the Mac OS X hostname
created: 2025-09-21 11:06:39
updated: 2025-09-21 11:21:39
tags:
  - osx
  - network
---
Periodically my Mac hostname appears to go *walkabout*. I've yet to resolve why, and have lost the will look very carefully (I think it's a DNS/DHCP issue). Changing it via System Settings does not always work. 

In the meantime, re-setting the hostname can easily be achieved from the command line.

There are *three* potential hostnames that can be set or retrieved:

- **HostName** … which is the primary hostname and should be fully qualified *e.g.* `MyMac.local` (if not accessible over the internet) or `swarms.theapiarist.org`.
- **LocalHostName** … which is the name used on the local network, the Bonjour hostname, for file sharing *e.g.* `MyMac.local`, when setting this omit the domain and the system automagically appends `.local`.
- **ComputerName** … the computer name, which lacks any domain information, and is the name used by the Finder *e.g.* `MyMac`

The current names can be retrieved using:

`sudo scutil --get <Name>` where `<Name>` is one of the words in bold in the list above *e.g.* `sudo scutil --get LocalHostName`

And can be changed using: 

`sudo scutil --set <Name> <new host name>` *e.g.* `sudo scutil --set ComputerName MyMac`

After setting a new hostname flush the DNS cache using:

`dscacheutil -flushcache`

The hostname appears to be set in at least two separate locations, and `echo $HOSTNAME` only returns one of them. Being OS X, there's no `/etc/hostname` of course 😞.

Further information:

- An [old discussion on StackExchange](https://apple.stackexchange.com/questions/287760/set-the-hostname-computer-name-for-macos#287775) on setting the hostname from the command line
- More than you'd ever want to know about `scutil` is available by typing `man scutil` at the command prompt