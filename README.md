# SOC Home Lab — Splunk + Windows Event Logs

## Overview
I built this home lab to simulate a SOC environment and practice 
detecting common attack techniques. I used Splunk, Sysmon, and 
Windows Event Logs across two VMs to replicate a real monitoring 
pipeline. This project helped me understand how logs flow from a 
Windows endpoint to a SIEM and how to build detections and alerts 
around suspicious activity.

## Tools Used
- VirtualBox
- Ubuntu 24 (SIEM)
- Windows 10 (Target)
- Splunk Enterprise 10.2.2
- Sysmon
- Splunk Universal Forwarder

## Architecture
I set up two VMs on the same NAT network in VirtualBox. The Windows 
10 VM acts as the target endpoint and forwards logs to Splunk running 
on the Ubuntu VM via the Universal Forwarder on port 9997.Windows 10 VM → Universal Forwarder → Ubuntu VM (Splunk) port 9997

## Detections Built
I built four detections covering different stages of an attack:

| Detection | Event ID | Source | Tactic |
|---|---|---|---|
| Encoded PowerShell Command | 4104 | PowerShell Operational | Obfuscation |
| Suspicious Web Request | 4104 | PowerShell Operational | Payload Delivery |
| Failed Login / Brute Force | 4625 | Windows Security | Brute Force |
| Reconnaissance - whoami | 1 | Sysmon | Reconnaissance |

## Alerts
I configured all four detections as real-time Splunk alerts with 
tuned thresholds and throttling to reduce noise. All alerts log 
to Triggered Alerts in Splunk.

## Incident Reports
- [IR-001 Encoded PowerShell](incident-reports/IR-001-encoded-powershell.md)
- [IR-002 Suspicious Web Request](incident-reports/IR-002-web-request.md)
- [IR-003 Brute Force Login](incident-reports/IR-003-brute-force.md)
- [IR-004 whoami Recon](incident-reports/IR-004-whoami-recon.md)

## Setup Guides
- [Splunk on Ubuntu](setup/splunk-ubuntu-install.md)
- [Windows Forwarder Setup](setup/windows-forwarder-setup.md)
- [Sysmon Setup](setup/sysmon-setup.md)

## Screenshots
Screenshots for each detection are included in their respective 
detection files in the /detections folder.
