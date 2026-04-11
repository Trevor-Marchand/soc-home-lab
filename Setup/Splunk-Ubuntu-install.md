# Splunk Installation — Ubuntu VM

## VM Specifications
- OS: Ubuntu 24
- RAM: 4-8 GB
- CPU: 2 cores
- Disk: 30 GB

## Installation Steps

### 1. Update System
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install wget -y
```

### 2. Download Splunk
```bash
wget -O splunk.deb "https://download.splunk.com/products/splunk/releases/9.2.0/linux/splunk-9.2.0-*.deb"
```

### 3. Install Splunk
```bash
sudo dpkg -i splunk.deb
```

### 4. Start Splunk
```bash
sudo /opt/splunk/bin/splunk start --accept-license
```

### 5. Enable Auto-Start
```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

### 6. Access Splunk Web
http://<Ubuntu-IP>:8000

## Enable Log Receiving
1. Login to Splunk Web
2. Go to Settings → Forwarding and Receiving
3. Click Configure Receiving
4. Click Add New
5. Enter port: 9997
6. Click Save
