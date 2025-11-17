# linux-BashScript-SystemMonitoring
#!/bin/bash

# --- System Health Snapshot Script ---
# Author: Naveen
# Date: 2025-11-17
# Description: Gathers CPU info, memory usage, disk space, and I/O stats.

echo "=========================================="
echo "          SYSTEM HEALTH SNAPSHOT          "
echo "=========================================="
echo ""

# 1. CPU Architecture Information
echo "### 1. CPU Architecture (lscpu) ###"
lscpu | head -n 10
echo ""

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
