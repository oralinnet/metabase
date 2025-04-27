# Metabase Installation Guide for Linux

## Prerequisites
- JDK-21 (Download from [Google_drive](https://drive.google.com/file/d/135nJUiWLfSns_z_Xtlr3pnPwaFDGIR8D/view?usp=sharing))
- Metabase JAR file (Download from [Google_drive](https://drive.google.com/file/d/138qdZGcew9fNPgbkeLz_LY66i5en45MX/view?usp=sharing))

## 1. Install JDK-21
```bash
# Create JDK directory
mkdir /opt/jdk-21

# Extract JDK archive
tar -xvzf openlogic-openjdk-21.0.6+7-linux-x64.tar.gz
cd openlogic-openjdk-21.0.6+7-linux-x64/
mv * /opt/jdk-21/

# Verify Java installation
/opt/jdk-21/bin/java --version
```

## 2. Create Metabase User and Directory Structure
```bash
# Create metabase group and user
groupadd --system metabase
useradd --system -g metabase --no-create-home metabase

# Create necessary directories and files
mkdir -p /opt/metabase
touch /var/log/metabase.log
touch /etc/default/metabase

# Set proper permissions
chown -R metabase:metabase /opt/metabase
chown metabase:metabase /var/log/metabase.log
chmod 640 /etc/default/metabase
```

## 3. Configure Logging
```bash
# Create rsyslog configuration for Metabase
cat << EOF > /etc/rsyslog.d/metabase.conf
:msg,contains,"metabase" /var/log/metabase.log
& stop
EOF

# Restart rsyslog service
systemctl restart rsyslog
```

## 4. Install Metabase
```bash
# Navigate to Metabase directory
cd /opt/metabase

# Upload metabase.jar file to this directory
# Then set proper ownership
chown -R metabase:metabase /opt/metabase
```

## 5. Create Systemd Service
Create a systemd service file at `/etc/systemd/system/metabase.service`:

```ini
[Unit]
Description=Metabase server
After=syslog.target
After=network.target

[Service]
WorkingDirectory=/opt/metabase/
ExecStart=/opt/jdk-21/bin/java -jar /opt/metabase/metabase.jar
EnvironmentFile=/etc/default/metabase
User=metabase
Type=simple
StandardOutput=syslog
StandardError=syslog
SyslogIdentifier=metabase
SuccessExitStatus=143
TimeoutStopSec=120
Restart=always

[Install]
WantedBy=multi-user.target
```

## 6. Start and Enable Metabase
```bash
# Reload systemd daemon
systemctl daemon-reload

# Start Metabase service
systemctl start metabase

# Enable Metabase to start on boot
systemctl enable metabase

# Check service status
systemctl status metabase
```

## 7. Firewall Configuration
```bash
# Open port 3000 in firewall
# Use appropriate command for your firewall (e.g., ufw, firewalld)
```

## Notes
- Metabase runs on port 3000 by default
- Make sure to configure your firewall appropriately
- Configure Selinux for metabase 
- Check logs at `/var/log/metabase.log` if you encounter any issues