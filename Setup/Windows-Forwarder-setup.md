# Splunk Universal Forwarder Setup — Windows 10

## VM Specifications
- OS: Windows 10
- RAM: 4 GB
- CPU: 2 cores
- Disk: 40 GB

## Installation

### 1. Download Forwarder
Download Splunk Universal Forwarder from:
https://www.splunk.com/en_us/download/universal-forwarder.html

### 2. Install via PowerShell (Admin)
```powershell
msiexec.exe /i splunkforwarder.msi AGREETOLICENSE=Yes /quiet
```

### 3. Configure Forwarder
```powershell
cd "C:\Program Files\SplunkUniversalForwarder\bin"

# Connect to Splunk server
.\splunk.exe add forward-server :9997

# Add Windows Event Logs
.\splunk.exe add monitor "WinEventLog://Security"
.\splunk.exe add monitor "WinEventLog://System"
.\splunk.exe add monitor "WinEventLog://Application"

# Start forwarder
.\splunk.exe start
```

## Configure inputs.conf
Navigate to:
C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf

Add the following:
```ini
[WinEventLog://Application]
disabled = 0
index = windows
start_from = oldest
current_only = 0
checkpointInterval = 5

[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0
index = windows
start_from = oldest
current_only = 0
checkpointInterval = 5
renderXml = false

[WinEventLog://System]
disabled = 0
index = windows
start_from = oldest
current_only = 0
checkpointInterval = 5
renderXml = false

[WinEventLog://Security]
disabled = 0
index = windows
start_from = oldest
current_only = 0
checkpointInterval = 5
renderXml = false

[WinEventLog://Microsoft-Windows-PowerShell/Operational]
disabled = 0
index = windows
start_from = oldest
current_only = 0
checkpointInterval = 5
renderXml = false
```

### Restart Forwarder
```powershell
Restart-Service SplunkForwarder
```

## Verify Connection
In Splunk Web run:
index="windows" | stats count by sourcetype
All configured log sources should appear.
