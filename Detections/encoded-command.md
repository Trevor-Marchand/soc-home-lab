# Detection: Suspicious Encoded PowerShell Command

## Search Query
index="windows" source="wineventlog:microsoft-windows-powershell/operational"
EventCode=4104 Message="Write-Host"

## What It Detects
Execution of Base64 encoded PowerShell commands using the 
-EncodedCommand flag. Commonly used by attackers to obfuscate 
malicious scripts.

## Event Details
- Log: Microsoft-Windows-PowerShell/Operational
- EventCode: 4104
- Key Field: Message

## Alert Settings
- Run every: 5 minutes
- Time range: Last 5 minutes
- Trigger: Number of results > 0
- Severity: High
- Throttle: 60 minutes

## Screenshot
![Encoded Command Detection](../screenshots/encoded-command-splunk.png)
