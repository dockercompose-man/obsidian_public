```bash
#!/bin/bash

# Define log file name
LOG_FILE="/var/log/security-updates-$(date +%Y-%m-%d-%H-%M-%S).log"

# Update package lists
echo "Updating package lists at $(date)" >> "$LOG_FILE"
yum -y updateinfo 2>&1 | tee -a "$LOG_FILE"

# Upgrade only security updates
echo "Upgrading security updates at $(date)" >> "$LOG_FILE"
yum -y --security update 2>&1 | tee -a "$LOG_FILE"
```
