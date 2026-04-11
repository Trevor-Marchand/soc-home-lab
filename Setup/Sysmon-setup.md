# Sysmon Installation — Windows 10

## Why I Installed Sysmon
The default Windows Event Logs don't provide enough detail for 
effective threat detection. I installed Sysmon to get richer 
telemetry including process creation, command-line arguments, 
and parent process information which are essential for detecting 
reconnaissance and lateral movement.

## What I Did

### 1. Downloaded Sysmon
I downloaded Sysmon from Microsoft Sysinternals:
https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

### 2. Installed Sysmon
I installed it via PowerShell running as Administrator:
```powershell
Sysmon64.exe -accepteula -i
```

### 3. Verified the Installation
```powershell
Get-Service Sysmon64
```
The status showed Running confirming it installed correctly.

## Key Event IDs I Used
| Event ID | Description |
|---|---|
| 1 | Process Creation |
| 3 | Network Connection |
| 7 | Image Loaded |
| 11 | File Created |
| 13 | Registry Value Set |

## Enabling PowerShell Script Block Logging
I also enabled PowerShell Script Block Logging so that Splunk 
could capture the decoded content of encoded PowerShell commands. 
Without this Event ID 4104 would not be generated:
```powershell
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" /v EnableScriptBlockLogging /t REG_DWORD /d 1 /f
```

I also enabled Module Logging for additional PowerShell visibility:
```powershell
reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ModuleLogging" /v EnableModuleLogging /t REG_DWORD /d 1 /f
```

## Verifying Logging Was Active
I confirmed Script Block Logging was enabled by checking the registry:
```powershell
Get-ItemProperty "HKLM:\SOFTWARE\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging"
```
EnableScriptBlockLogging showed a value of 1 confirming it was active.

## Verifying in Splunk
I confirmed Sysmon events were flowing into Splunk with:
```
index="windows" source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
| stats count by EventCode
```
