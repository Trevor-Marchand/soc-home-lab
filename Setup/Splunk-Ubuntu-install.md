# Splunk Installation — Ubuntu VM

## VM Specifications
I configured the Ubuntu VM with the following specs to comfortably 
run Splunk:
- OS: Ubuntu 24
- RAM: 4-8 GB
- CPU: 2 cores
- Disk: 30 GB

## What I Did

### 1. Updated the System
Before installing anything I updated the Ubuntu VM to make sure 
all packages were current:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install wget -y
```

### 2. Downloaded Splunk
I downloaded the Splunk .deb package directly from Splunk's website:
```bash
wget -O splunk.deb "https://download.splunk.com/products/splunk/releases/9.2.0/linux/splunk-9.2.0-*.deb"
```

### 3. Installed Splunk
```bash
sudo dpkg -i splunk.deb
```

### 4. Started Splunk and Accepted the License
```bash
sudo /opt/splunk/bin/splunk start --accept-license
```

### 5. Enabled Auto-Start
I enabled Splunk to start automatically on boot so I wouldn't 
need to manually start it every time:
```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

### 6. Accessed Splunk Web
Once installed I accessed the Splunk web interface at:
http://<Ubuntu-IP>:8000

## Enabling Log Receiving
To allow the Windows forwarder to send logs I configured Splunk 
to listen on port 9997:
1. Went to Settings → Forwarding and Receiving
2. Clicked Configure Receiving
3. Clicked Add New
4. Entered port 9997
5. Clicked Save
