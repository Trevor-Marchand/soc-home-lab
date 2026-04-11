# IR-003 — Brute Force Login Attempt

**Date:** April 10, 2026
**Severity:** Medium
**Host:** DESKTOP-3R2G504

## Summary
Multiple failed login attempts were detected on a Windows 10 endpoint 
indicating a possible brute force attack against a local user account.

## What Was Detected
Event ID 4625 (Failed Logon) was triggered multiple times within a short 
time window. Splunk alert fired after exceeding the threshold of 5 failed 
login attempts.

## Evidence
- EventCode: 4625
- Source: WinEventLog:Security
- ComputerName: DESKTOP-3R2G504
- Logon_Type: 0
- 7 failed login events detected

## Conclusion
The repeated failed authentication attempts suggest a brute force or 
credential stuffing attack targeting a local account. No successful 
logon (Event ID 4624) was observed following the failures.

## Recommended Response
- Lock the targeted account
- Block the source IP if external
- Review all 4624 events following the failures
- Enable account lockout policy
