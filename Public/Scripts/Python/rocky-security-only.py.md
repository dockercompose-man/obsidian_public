```python
import subprocess
import datetime

now = datetime.datetime.now()
LOG_FILE = f"/var/log/security-updates-{now.year}-{now.month}-{now.day}-{now.hour}-{now.minute}-{now.second}.log"

# open log file
log_file = open(LOG_FILE, "a")

# Update package lists
log_file.write(f"Updating package lists at {now}\n")
subprocess.run(["dnf", "check-update", "--security"])

# Upgrade only security updates
log_file.write(f"Upgrading security updates at {datetime.datetime.now()}\n")
subprocess.run(["dnf", "update", "--security", "--advisory=RHSA-*"])

# close log file
log_file.close()

# open the log file in read mode and print its contents
with open(LOG_FILE, "r") as log_file:
    print(log_file.read())
```

##### This script uses the dnf command to check for the package lists and then upgrade only the packages that are marked as security updates. The dnf check-update --security command lists the security updates available and the script passes the output of this command to the dnf update --security --advisory=RHSA-* command to upgrade only those packages. The --advisory=RHSA-* option specifies that only Red Hat Security Advisory (RHSA) type updates should be considered.