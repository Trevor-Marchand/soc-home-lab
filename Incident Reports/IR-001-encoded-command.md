# IR-001 — Suspicious Encoded PowerShell Command Executed

**Date:** April 10, 2026
**Severity:** High
**Host:** DESKTOP-3R2G504

## Summary
A Base64 encoded PowerShell command was executed on a Windows 10 
endpoint using the -EncodedCommand flag. This technique is commonly 
used by attackers to obfuscate malicious scripts and bypass basic 
security controls.

## What Was Detected
Event ID 4104 (Script Block Logging) captured a PowerShell command 
executed via the -EncodedCommand flag. Script Block Logging decoded 
the content and logged it to the PowerShell Operational log.

## Evidence
- EventCode: 4104
- Source: WinEventLog:Microsoft-Windows-PowerShell/Operational
- ComputerName: DESKTOP-3R2G504
- Message contained: EncodedCommand flag
- 6 events detected

## Conclusion
The use of -EncodedCommand is a known attacker technique used to 
hide malicious intent from basic string-based detections. While the 
decoded content in this case was benign (lab test), this pattern 
warrants immediate investigation in a production environment.

## Recommended Response
- Decode and analyze the full script block content
- Check ParentProcess to determine what spawned PowerShell
- Review surrounding timeline for additional suspicious activity
- Consider blocking -EncodedCommand via PowerShell Constrained Language Mode
