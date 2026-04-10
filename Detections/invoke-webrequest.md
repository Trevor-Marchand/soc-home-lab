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

## Screenshot
<img width="1281" height="823" alt="Invoke WebRequest" src="https://github.com/user-attachments/assets/39ed7c3f-6b39-48f4-a7e5-a876afd1e7ee" />
