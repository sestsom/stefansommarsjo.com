+++
author = "Stefan Sommarsjö"
title = "PowerShell script to monitor CPU usage"
date = "2023-07-27"
description = "PowerShell script to monitor CPU usage"
tags = [
    "PowerShell",
	"Developing",
]
categories = [
    "Developing",
]
series = ["Developing"]
aliases = ["PowerShell-script-to-monitor-cpu-usage"]
draft = true
+++

### Sons game freezes.
Son complains about Fortnite and Valorant occasionally freezes during gaming and it causes some rage :-).

I suspect  the culprit lies in the CPU usage of certain processes running in the background.

### Hello PowerShell.
The script designed to monitor the CPU usage of all active processes on your PC. The script will only report 
processes that consume CPU usage beyond a certain threshold. If you can identify processes that use too much 
CPU, you can shut them down or manage them appropriately to prevent your PC from freezing during gaming.
<!--more-->
## Execution policy.
Firstly, PowerShell has a feature called "execution policy", which controls the conditions under which PowerShell loads configuration files and runs scripts. If you get an error "..running scripts is disabled", That error message means that your current execution policy doesn't allow running the script.

To solve this issue, you can change the execution policy. Here are the steps:

1. Open PowerShell as an administrator. You can do this by searching for PowerShell in the start menu, right-clicking on it, and selecting "Run as administrator".

2. Check the current execution policy by typing 

```PowerShell
Get-ExecutionPolicy
```

3. If the policy is not set to RemoteSigned or Unrestricted, you can change the execution policy by typing ```Set-ExecutionPolicy RemoteSigned```. This policy allows local scripts to run without a digital signature, but downloaded scripts must be signed by a trusted publisher.

You'll see a prompt asking to confirm the change, to which you can reply **Y for Yes** or A for Yes to All.

Keep in mind that these steps change the execution policy for all PowerShell sessions. If you want to change the execution policy for only the current session, you can do so by adding -Scope Process to the command:

```PowerShell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```






