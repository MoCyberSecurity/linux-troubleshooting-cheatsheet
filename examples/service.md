# 🖥 CPU Issues / High Load  
### Linux Troubleshooting Cheat Sheet — Practical Investigation Steps

This guide helps diagnose **high CPU usage, stuck processes, or overall system slowness**.

---

# 🚀 1. Check CPU Load

**Commands:**  
*`top`* — Interactive view of CPU, memory, and processes  
*`htop`* — Enhanced top with process tree (if installed)  
*`uptime`* — Load averages over 1, 5, 15 minutes  

---

# 📊 2. Identify CPU-Heavy Processes

**Commands:**  
*`ps aux --sort=-%cpu | head -20`* — Top 20 CPU-consuming processes  
*`pidstat 1`* — CPU usage per process live  
*`mpstat -P ALL 1`* — CPU usage per core  

---

# 🧩 3. Inspect Process Behavior

**Commands:**  
*`strace -p <PID>`* — Trace system calls of a process  
*`lsof -p <PID>`* — Open files by process  
*`renice -n <value> -p <PID>`* — Change process priority  

---

# 🖤 Memory Issues / High Usage  
### Linux Troubleshooting Cheat Sheet — Practical Investigation Steps

This guide helps diagnose **memory leaks, swap issues, or overall high memory usage**.

---

# 🚀 1. Check Memory Usage

**Commands:**  
*`free -h`* — Show memory and swap usage  
*`vmstat 1`* — Real-time memory stats  
*`cat /proc/meminfo`* — Detailed memory info  

---

# 📊 2. Identify Memory-Heavy Processes

**Commands:**  
*`top`* (sort by `%MEM`) — Interactive view  
*`ps aux --sort=-%mem | head -20`* — Top 20 memory consumers  
*`smem -r`* — Reports per process memory usage (if installed)  

---

# 🧩 3. Inspect Swap Usage

**Commands:**  
*`swapon -s`* — Active swap areas  
*`free -h`* — Swap utilization  
*`vmstat 1`* — Swap activity over time  

---

# 🛠 Services / Daemon Troubleshooting  
### Linux Troubleshooting Cheat Sheet — Practical Investigation Steps

This guide helps diagnose **services failing, not starting, or behaving incorrectly**.

---

# 🚀 1. Check Service Status

**Commands:**  
*`systemctl status <service>`* — Detailed service status  
*`service <service> status`* — Legacy command for status  
*`systemctl is-active <service>`* — Simple active/inactive check  

---

# 🔍 2. Inspect Logs for Services

**Commands:**  
*`journalctl -u <service> --no-pager --since "2h ago"`* — Service logs  
*`tail -f /var/log/<service>/<logfile>`* — Follow service logs live  
*`dmesg | grep <service>`* — Kernel messages related to the service  

---

# 🛠 3. Start / Stop / Restart Services

**Commands:**  
*`sudo systemctl start <service>`* — Start service  
*`sudo systemctl stop <service>`* — Stop service  
*`sudo systemctl restart <service>`* — Restart service  
*`sudo systemctl reload <service>`* — Reload configuration without stopping  

---

# 🧩 4. Enable / Disable Services at Boot

**Commands:**  
*`sudo systemctl enable <service>`* — Enable service at boot  
*`sudo systemctl disable <service>`* — Disable service at boot  

---

# ⚙️ 5. Check Dependencies

**Commands:**  
*`systemctl list-dependencies <service>`* — See required services  
*`systemctl show <service>`* — Detailed properties and environment  

---

# 🚀 6. Inspect Open Ports for Services

**Commands:**  
*`ss -tulnp | grep <service>`* — Which ports the service is listening on  
*`netstat -tulnp | grep <service>`* — Alternative if `ss` not available  
