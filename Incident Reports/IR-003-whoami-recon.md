# IR-003 — Post-Exploitation Reconnaissance - whoami Detected

**Date:** April 10, 2026
**Severity:** Medium
**Host:** DESKTOP-3R2G504

## Summary
Execution of whoami.exe was detected on a Windows 10 endpoint via 
Sysmon process creation logging. whoami is commonly executed by 
attackers immediately after gaining access to enumerate the current 
user context and privilege level.

## What Was Detected
Sysmon Event ID 1 (Process Creation) captured the execution of 
whoami.exe. The parent process was identified as PowerShell indicating 
the command was run from a PowerShell session.

## Evidence
- EventCode: 1
- Source: WinEventLog:Microsoft-Windows-Sysmon/Operational
- ComputerName: DESKTOP-3R2G504
- User: DESKTOP-3R2G504\Trevo
- CommandLine: whoami.exe
- ParentImage: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
- 6 events detected

## Conclusion
The execution of whoami.exe from a PowerShell parent process is 
consistent with post-exploitation reconnaissance behavior. An attacker 
who has gained a foothold will typically run whoami as one of their 
first commands to understand their privilege level.

## Recommended Response
- Investigate how PowerShell was initially launched
- Review full process tree around the whoami execution
- Check for privilege escalation attempts following the recon
- Correlate with other alerts from the same host and timeframe
- Look for lateral movement indicators
