# Alert Configurations

I configured all three detections as real-time Splunk alerts. I 
chose real-time alerting for this lab to get immediate notification 
of suspicious activity. I also tuned the thresholds and throttling 
for each alert to reduce noise while maintaining detection coverage.

| Alert | Schedule | Threshold | Severity | Throttle |
|---|---|---|---|---|
| Failed Login | Real-Time | > 5 | Medium | 30 min |
| Invoke-WebRequest | Real-Time | > 0 | High | 60 min |
| whoami Recon | Real-Time | > 0 | Medium | 60 min |

All alerts are configured to:
- Add to Triggered Alerts
- Expiration: 24 hours

> Note: I used real-time alerts in this lab for immediate detection. 
> In a production SOC scheduled alerts are often preferred to reduce 
> system load on the SIEM.

## Screenshot

