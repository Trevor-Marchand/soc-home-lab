# Detection: Reconnaissance Command — whoami

## Why I Built This Detection
whoami.exe is one of the first commands an attacker runs after 
gaining access to a system to identify what user context and 
privilege level they have. I chose to detect this via Sysmon 
rather than PowerShell logs because Sysmon catches whoami 
regardless of how it was launched — whether from CMD, PowerShell, 
or another process. It also provides richer data including the 
parent process which helps identify how the command was invoked.

## Search Query
index="windows" source="wineventlog:microsoft-windows-sysmon/operational"
EventCode=1 Image="whoami"
| table _time, ComputerName, User, CommandLine, ParentImage, ParentCommandLine
| sort -_time

## Why I Used Sysmon Event ID 1
Sysmon Event ID 1 captures process creation events with full 
command-line arguments and parent process information. This gave 
me visibility into not just that whoami was run but what process 
launched it which is critical context for an investigation.

## Alert Settings
- Schedule: Real-time
- Trigger: Number of results > 0
- Severity: Medium
- Throttle: 60 minutes
- Action: Add to Triggered Alerts
- Expiration: 24 hours

## Screenshot
<img width="1282" height="801" alt="whoami" src="https://github.com/user-attachments/assets/21788a11-207c-4cd1-a279-5637e1d4a4b4" />
