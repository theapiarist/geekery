---
title:
created:
updated:
draft: "false"
tags:
  - raspberrypi
---
Identify hardware by SSH using `cat /sys/firmware/devicetree/base/model`

Memory `free h`

OS `lsb_release -a` or `cat /etc/os-release`

%%

And here's script from [here](https://devguide.dev/blog/raspberry-pi-identify-hardware) that lists that lot (and more) for convenience:

```
echo '#!/bin/bash
echo "=== Raspberry Pi Hardware Info ==="
echo "Model: $(cat /sys/firmware/devicetree/base/model)"
echo "RAM: $(free -h | awk '\''/^Mem:/ {print $2}'\'')"
echo "CPU: $(lscpu | grep '\''Model name'\'' | cut -d: -f2 | xargs)"
echo "Cores: $(nproc)"
echo "OS: $(lsb_release -ds 2>/dev/null || cat /etc/os-release | grep PRETTY_NAME | cut -d= -f2 | tr -d '\''"'\'')"' > ~/pi-info.sh && chmod +x ~/pi-info.sh
```

%%