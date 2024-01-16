+++
author = "Stefan Sommarsjö"
title = "Distro hopping and Pipewire annoyances"
date = "2023-05-03"
description = "Distro hopping and Pipewire annoyances"
tags = [
    "Linux",
	"Pipewire",
]
categories = [
    "Linux",
]
series = ["Linux"]
aliases = ["distro-hopping-and-pipewire-annoyances"]
draft = false
+++

**Distro hopping**.
First off. I've switched to Fedora 38 now, lets see how long it will last. I wouldn't be surprised if I'm back to Debian or Kali in a really near future :-).

**Pipewire annoyances**.
For as long as I can remember I've always had this issues with the sound on Linux. Random "popping" in the speakers.
Since I most of the time use a Bluetooth headset I've ignored the problem.
Had no better to do for a while so I spent some time looking it up and finally found a solution that work.

Copy existing alsa config script so we can finger it a little bit...
<!--more-->

```bash
sudo cp -a /usr/share/wireplumber/main.lua.d/50-alsa-config.lua /etc/wireplumber/main.lua.d/50-alsa-config.lua
```

```bash
sudo vi /etc/wireplumber/main.lua.d/50-alsa-config.lua
```

Locate this row and replace 5 with a 0 for disabling suspend on idle. By default it's commented out so remove the **--**.
```lua
--["session.suspend-timeout-seconds"] = 5,  -- 0 disables suspend
```

Restart your computer and Voila, problem solved.



