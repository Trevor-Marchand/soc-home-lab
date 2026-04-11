# Splunk Universal Forwarder Setup — Windows 10

## VM Specifications
I configured the Windows 10 VM as the target endpoint:
- OS: Windows 10
- RAM: 4 GB
- CPU: 2 cores
- Disk: 40 GB

## What I Did

### 1. Downloaded the Universal Forwarder
I downloaded the Splunk Universal Forwarder for Windows from:
https://www.splunk.com/en_us/download/universal-forwarder.html

### 2. Installed the Forwarder
I installed it silently via PowerShell running as Administrator:
```powershell
msiexec.exe /i splunkforwarder.msi AGREETOLICENSE=Yes /quiet
```

### 3. Connected the Forwarder to Splunk
I pointed the forwarder to my Ubuntu Splunk instance and added 
the core Windows event log sources:
```powershell
cd "C:\Program Files\SplunkUniversalForwarder\bin"

.\splunk.exe add forward-server :9997

.\splunk.exe add monitor "WinEventLog://Security"
.\splunk.exe add monitor "WinEventLog://System"
.\splunk.exe add monitor "WinEventLog://Application"

.\splunk.exe start
```

### 4. Configured inputs.conf
I manually edited inputs.conf to add the PowerShell Operational 
and Sysmon logs which are not added by default. This was an 
important step because without this Event ID 4104 would not 
be collected:
```
C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf
```

<img width="1009" height="768" alt="Inputs" src="https://github.com/user-attachments/assets/8c1b4bb2-4a21-4fdb-84dc-95db55a65f46" />




### 5. Restarted the Forwarder
After updating inputs.conf I restarted the forwarder to apply 
the changes:
```powershell
Restart-Service SplunkForwarder
```

## Verifying the Connection
I confirmed logs were flowing into Splunk by running:
index="windows" | stats count by sourcetype
All configured log sources appeared in the results confirming 
the pipeline was working correctly.
