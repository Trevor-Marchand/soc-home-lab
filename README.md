# SOC Home Lab — Splunk + Windows Event Logs

A home lab simulating a SOC environment to detect common attack 
techniques using Splunk, Sysmon, and Windows Event Logs.

## Tools Used
- VirtualBox
- Ubuntu 24 (SIEM)
- Windows 10 (Target)
- Splunk Enterprise 10.2.2
- Sysmon
- Splunk Universal Forwarder

## Architecture
Ubuntu VM (Splunk SIEM) ← port 9997 ← Windows 10 VM (Target + Forwarder)

## Detections Built
| Detection | Event ID | Source |
|---|---|---|
| Encoded PowerShell Command | 4104 | PowerShell Operational |
| Failed Login / Brute Force | 4625 | Windows Security |
| Suspicious Web Request | 4104 | PowerShell Operational |
| Reconnaissance - whoami | 1 | Sysmon |

## Alerts
All 4 detections have been configured as Splunk alerts with:
- Trigger threshold tuned per detection
- Severity levels assigned
- Results logged to Triggered Alerts

## Incident Reports
- [IR-001 Brute Force Login](incident-reports/IR-001-brute-force.md)
- [IR-002 Encoded PowerShell](incident-reports/IR-002-encoded-powershell.md)
- [IR-003 Suspicious Web Request](incident-reports/IR-003-web-request.md)
- [IR-004 whoami Recon](incident-reports/IR-004-whoami-recon.md)

## Setup Guides
- [Splunk on Ubuntu](setup/splunk-ubuntu-install.md)
- [Windows Forwarder Setup](setup/windows-forwarder-setup.md)
- [Sysmon Setup](setup/sysmon-setup.md)

## Screenshots
Screenshots for each detection are included in their 
respective detection files in the /detections folder.
