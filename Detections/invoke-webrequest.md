# Detection: Suspicious PowerShell Web Request

## Search Query
index="windows" source="wineventlog:microsoft-windows-powershell/operational"
Message="Invoke-WebRequest"

## What It Detects
Use of Invoke-WebRequest in PowerShell to download files from 
external URLs. Commonly used to download malware payloads.

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
