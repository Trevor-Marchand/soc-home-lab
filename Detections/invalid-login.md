# Detection: Failed Login Attempt

## Search Query
index="windows" source="WinEventLog:Security" EventCode=4625
| stats count by Account_Name, Source_Network_Address
| where count > 5
| sort -count

## What It Detects
Repeated failed authentication attempts indicating a possible 
brute force or credential stuffing attack.

## Event Details
- Log: Windows Security
- EventCode: 4625
- Key Fields: Account_Name, Logon_Type, Failure_Reason

## Alert Settings
- Run every: 15 minutes
- Time range: Last 15 minutes
- Trigger: Number of results > 5
- Severity: Medium
- Throttle: 30 minutes

## Screenshot
<img width="1280" height="798" alt="Invalid Login" src="https://github.com/user-attachments/assets/f1684cc8-c7d3-478b-9a8d-c6f55f176a73" />
