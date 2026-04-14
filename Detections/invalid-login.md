# Detection: Failed Login / Brute Force Attempt

## Why I Built This Detection
Failed login attempts are one of the most common indicators of a 
brute force attack. I built this detection to alert when a single 
account accumulates more than 5 failed logins within a 15 minute 
window which is a strong indicator of automated credential stuffing 
or brute force activity.

## Search Query
index="windows" source="WinEventLog:Security" EventCode=4625

## Why I Used Event ID 4625
Event ID 4625 is the standard Windows failed logon event. I used 
the stats command to group failures by account name and source 
address so the alert only fires when a pattern of failures is 
detected rather than a single mistyped password.

## Alert Settings
- Schedule: Real-time
- Trigger: Number of results > 5
- Severity: Medium
- Throttle: 30 minutes
- Action: Add to Triggered Alerts
- Expiration: 24 hours

## Screenshot
<img width="1280" height="798" alt="Invalid Login" src="https://github.com/user-attachments/assets/f1684cc8-c7d3-478b-9a8d-c6f55f176a73" />
