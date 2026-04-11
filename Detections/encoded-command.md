# Detection: Suspicious Encoded PowerShell Command

## Search Query
index="windows" source="wineventlog:microsoft-windows-powershell/operational" 
EventCode=4104 Message="*EncodedCommand*"

## What It Detects
Detects the use of the -EncodedCommand flag in PowerShell which is 
used to execute Base64 encoded commands. This is a common obfuscation 
technique used by attackers to hide malicious scripts from basic 
string-based detections.

## Event Details
- Log: Microsoft-Windows-PowerShell/Operational
- EventCode: 4104
- Key Field: Message

## Alert Settings
- Trigger: Number of results > 0
- Severity: High
- Throttle: 60 minutes

## Screenshot
<img width="1284" height="822" alt="Encoded Command" src="https://github.com/user-attachments/assets/1306bdce-2232-4bd5-a763-de4f2eba143c" />
