# Detection: Reconnaissance Command — whoami

## Search Query
index="windows" source="wineventlog:microsoft-windows-sysmon/operational"
EventCode=1 Image="whoami"
| table _time, ComputerName, User, CommandLine, ParentImage, ParentCommandLine
| sort -_time

## What It Detects
Execution of whoami.exe commonly used by attackers post-exploitation 
to enumerate current user context and privilege level.

## Event Details
- Log: Microsoft-Windows-Sysmon/Operational
- EventCode: 1 (Process Creation)
- Key Fields: Image, CommandLine, ParentImage

## Alert Settings
- Run every: 5 minutes
- Time range: Last 5 minutes
- Trigger: Number of results > 0
- Severity: Medium
- Throttle: 60 minutes

## Screenshot
<img width="1282" height="801" alt="whoami" src="https://github.com/user-attachments/assets/21788a11-207c-4cd1-a279-5637e1d4a4b4" />
