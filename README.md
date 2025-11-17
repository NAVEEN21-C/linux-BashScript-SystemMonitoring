# linux-BashScript-SystemMonitoring
#!/bin/bash

# --- System Health Snapshot Script ---
# Author: Naveen
# Date: 2025-11-17
# Description: Gathers CPU info, memory usage, disk space, and I/O stats.
<img width="902" height="564" alt="dc267b76-5111-42e7-91de-baf0821e268f" src="https://github.com/user-attachments/assets/b19f5b91-8013-4a6a-a0e5-d8e9dd98cc74" />

echo "=========================================="
echo "          SYSTEM HEALTH SNAPSHOT          "
echo "=========================================="
echo ""

# 1. CPU Architecture Information
echo "### 1. CPU Architecture (lscpu) ###"
lscpu | head -n 10
echo ""
<img width="1072" height="536" alt="2ba259dc-7358-432d-93a7-f974e22e1415" src="https://github.com/user-attachments/assets/060aafbd-e1e0-4518-894b-6f143a42b2ae" />

# 2. Memory Usage (free -m)
echo "### 2. Memory Usage (free -m) ###"
# -m displays results in MB
free -m
echo ""

# 3. Disk Space Usage (df -h)
echo "### 3. Disk Space (df -h) ###"
# -h displays results in human-readable format
df -h
echo ""

# 4. CPU and Device I/O Statistics (iostat)
echo "### 4. CPU and Disk I/O Statistics (iostat) ###"
# -c displays CPU stats, -d displays device stats, -k uses kilobytes
# Output for 1 second, then exit
if command -v iostat &> /dev/null
then
    iostat -cd 1 1
else
    echo "WARNING: iostat command not found. Install 'sysstat' package (sudo yum install sysstat or sudo apt install sysstat)."
fi
echo ""

echo "=========================================="
echo "     LIVE JOURNAL LOG (journalctl -f)     "
echo "=========================================="
echo "Press Ctrl + C to stop the live log stream."
echo ""

# 5. Live Log Stream
journalctl -f
