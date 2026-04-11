# Detection: Suspicious PowerShell Web Request

## Why I Built This Detection
Invoke-WebRequest is a common technique used by attackers to 
download malware payloads or communicate with C2 servers directly 
from PowerShell. I built this detection to catch any use of 
Invoke-WebRequest on the endpoint. I tested it using the EICAR 
test file as a safe simulation of a malware download.

## Search Query
index="windows" source="wineventlog:microsoft-windows-powershell/operational"
Message="Invoke-WebRequest"

## Why I Used the Message Field
During testing I discovered that in my environment the script block 
content is stored in the Message field rather than ScriptBlockText. 
This was an important troubleshooting step as the detection would 
have returned no results using the wrong field name.

## Alert Settings
- Schedule: Real-time
- Trigger: Number of results > 0
- Severity: High
- Throttle: 60 minutes
- Action: Add to Triggered Alerts
- Expiration: 24 hours

## Screenshot
<img width="1281" height="823" alt="Invoke WebRequest" src="https://github.com/user-attachments/assets/39ed7c3f-6b39-48f4-a7e5-a876afd1e7ee" />
