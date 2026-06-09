---
id: 20wqi7ue1d
slug: fixing-package-is-in-a-very-bad-inconsistent-state-apt-errors
title: Fixing “Package is in a very bad inconsistent state” apt errors
created: 2025-11-10 16:33:29
updated: 2025-11-10 16:33:52
tags:
  - debian
  - linux
  - software
---
Google Cloud got into a real pickle over installing google-cloud-cli using apt, leaving me with repeated *Package is in a very bad inconsistent state* errors every time I tried to run a `sudo apt full-upgrade`.

This fixed it:

```
sudo mv /var/lib/dpkg/info/<packagename>.* /tmp/
sudo dpkg --remove --force-remove-reinstreq <packagename>
sudo apt-get remove <packagename>
sudo apt-get autoremove && sudo apt-get autoclean
```

… which I [found here](https://askubuntu.com/questions/148715/how-to-fix-package-is-in-a-very-bad-inconsistent-state-error) (dated over 13 years ago 😄).