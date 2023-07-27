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
aliases = ["powershell-script-to-monitor-cpu-usage"]
draft = false
+++

### Sons game freezes.
Son complains about Fortnite and Valorant occasionally freezing during gaming and it causes some rage :-).

I suspect the culprit lies in the CPU usage of certain processes running in the background.


### Hello PowerShell.
The script is designed to monitor the CPU usage of all active processes on your PC. The script will only report 
processes that consume CPU usage beyond a certain threshold (50%). If you can identify processes that use too much 
CPU, you can shut them down or manage them appropriately to prevent your PC from freezing during gaming.
<!--more-->

### Execution policy.
Firstly, PowerShell has a feature called "**execution policy**", which controls the conditions under which PowerShell loads configuration files and runs scripts. If you get an error "..running scripts is disabled", That error message means that your current execution policy doesn't allow running the script.

To solve this issue, you can change the execution policy. Here are the steps:

1. Open PowerShell as an administrator. You can do this by searching for PowerShell in the start menu, right-clicking on it, and selecting "Run as administrator".

2. Check the current execution policy by typing ```Get-ExecutionPolicy```.

3. If the policy is not set to RemoteSigned or Unrestricted, you can change the execution policy by typing ```Set-ExecutionPolicy RemoteSigned```. This policy allows local scripts to run without a digital signature, but downloaded scripts must be signed by a trusted publisher.

You'll see a prompt asking to confirm the change, to which you can reply **Y for Yes** or A for Yes to All.

Keep in mind that these steps change the execution policy for all PowerShell sessions. If you want to change the execution policy for only the current session, you can do so by adding **-Scope Process** to the command:
```Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process```.


### The script.
```PowerShell
# Specify the CPU threshold.
$cpuThreshold = 50

# Loop it.
while ($true) {
    # Get running processes and their CPU usage. Ignore Idle process.
    $processes = Get-WmiObject -Query `
      "SELECT IDProcess, Name, PercentProcessorTime FROM Win32_PerfFormattedData_PerfProc_Process WHERE NOT Name='_Total' AND NOT Name='Idle'"

    # For each
    foreach ($process in $processes) {
        # Calculate CPU usage for process
        $cpuUsage = $process.PercentProcessorTime

        # If CPU usage exceeds threshold, output information about the process.
        if ($cpuUsage -gt $cpuThreshold) {
            Write-Output ("Process ID: {0}, Process Name: {1}, CPU Usage: {2}%" -f $process.IDProcess, $process.Name, $cpuUsage)
        }
    }

    # Get some sleep before next update.
    Start-Sleep -Seconds 2
}
``` 
Just start the script and let it run in the background.


### "This script suck!".
I'm sure there exist hundreds of applications/scripts doing this better, but out of the box stuff wouldn't let me learn anything and have fun while doing it.


### Github.
Script is also available in my Powershell_Scripts repo. [https://github.com/sestsom/Powershell_Scripts](https://github.com/sestsom/Powershell_Scripts).

 




