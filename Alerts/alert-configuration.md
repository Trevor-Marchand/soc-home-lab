# Alert Configurations

| Alert | Schedule | Threshold | Severity | Throttle |
|---|---|---|---|---|
| Encoded PowerShell | Every 5 min | > 0 | High | 60 min |
| Failed Login | Every 15 min | > 5 | Medium | 30 min |
| Invoke-WebRequest | Every 5 min | > 0 | High | 60 min |
| whoami Recon | Every 5 min | > 0 | Medium | 60 min |

All alerts configured to:
- Add to Triggered Alerts
- Expiration: 24 hours
