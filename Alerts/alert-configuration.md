# Alert Configurations

| Alert | Schedule | Threshold | Severity | Throttle |
|---|---|---|---|---|
| Encoded PowerShell | Real-Time | > 0 | High | 60 min |
| Failed Login | Real-Time | > 5 | Medium | 30 min |
| Invoke-WebRequest | Real-Time | > 0 | High | 60 min |
| whoami Recon | Real-Time | > 0 | Medium | 60 min |

All alerts configured to:
- Schedule: Real-Time
- Add to Triggered Alerts
- Expiration: 24 hours

## Screenshot
<img width="1276" height="797" alt="All Alerts" src="https://github.com/user-attachments/assets/54886bb7-dab2-4ffc-918d-b6f920e0273d" />
