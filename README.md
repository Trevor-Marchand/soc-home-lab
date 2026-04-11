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
on the Ubuntu VM via the Universal Forwarder on port 9997.
Windows 10 VM → Universal Forwarder → Ubuntu VM (Splunk) port 9997

## Detections Built
I built three detections covering different stages of an attack:

| Detection | Event ID | Source | Tactic |
|---|---|---|---|
| Suspicious Web Request | 4104 | PowerShell Operational | Payload Delivery |
| Failed Login / Brute Force | 4625 | Windows Security | Brute Force |
| Reconnaissance - whoami | 1 | Sysmon | Reconnaissance |

## Alerts
I configured all three detections as real-time Splunk alerts with 
tuned thresholds and throttling to reduce noise. All alerts log 
to Triggered Alerts in Splunk.

<img width="1283" height="800" alt="All Alerts" src="https://github.com/user-attachments/assets/e27522bd-1a65-4347-9760-021dab19ef45" />


## Triggered Alerts
After running attack simulations all three alerts fired successfully 
and were logged in Splunk's Triggered Alerts dashboard.

<img width="1279" height="801" alt="Triggered Alerts" src="https://github.com/user-attachments/assets/6c9b0db2-1773-4361-a290-cf04a9bc9a9b" />


## Incident Reports
- [IR-001 Suspicious Web Request](Incident%20Reports/IR-001-web-request.md)
- [IR-002 Brute Force Login](Incident%20Reports/IR-002-brute-force.md)
- [IR-003 whoami Recon](Incident%20Reports/IR-003-whoami-recon.md)

## Setup Guides
- [Splunk on Ubuntu](Setup/splunk-ubuntu-install.md)
- [Windows Forwarder Setup](Setup/windows-forwarder-setup.md)
- [Sysmon Setup](Setup/Sysmon-setup.md)

## Screenshots
Screenshots for each detection are included in their respective 
detection files in the /detections folder.
