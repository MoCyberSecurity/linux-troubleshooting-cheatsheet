# 🧩 Disk Issues / Storage Problems  
### Linux Troubleshooting Cheat Sheet — Practical Investigation Steps

This guide helps diagnose **low disk space, I/O errors, slow performance, or missing partitions** from a Linux system.

---

# 🚀 1. Check Disk Usage (Space Problems)

📌 First step when a server behaves strangely — check if you are out of space.

**Commands:**  
*`df -h`* — Show disk usage in human-readable form  
*`du -sh /path/*`* — Show folder sizes inside a directory  
*`du -sh .`* — Size of the current directory  

---

# 📁 2. Find Large Files & Folders

Identify which files are consuming space quickly.

**Commands:**  
*`find / -type f -size +500M 2>/dev/null`* — Find files over 500 MB  
*`du -ah / | sort -rh | head -20`* — Top 20 largest files/folders  

---

# 📦 3. Check Inodes (Too Many Small Files)

Systems can run out of inodes even if disk space looks free.

**Commands:**  
*`df -i`* — Check inode usage  
*`find /path -xdev -type f | wc -l`* — Count files  

---

# 🛠 4. Check Disk Health (SMART)

Useful for detecting failing disks.

**Commands:**  
*`sudo smartctl -a /dev/sda`* — Full SMART report  
*`sudo smartctl -H /dev/sda`* — Health status  

---

# 🧪 5. Test Read/Write Performance

Check if disk slowness is the cause.

**Commands:**  
*`dd if=/dev/zero of=/tmp/testfile bs=1G count=1 oflag=direct`* — Write speed  
*`hdparm -t /dev/sda`* — Read speed  

---

# 🔍 6. Check Open File Handles (Too Many Files Open)

High file handle usage can cause performance issues.

**Commands:**  
*`lsof | wc -l`* — Total open files  
*`lsof /path/to/file`* — Check which process opened a file  

---

# 🧩 7. Check Mounted Filesystems

Sometimes storage issues come from incorrectly mounted partitions.

**Commands:**  
*`mount | column -t`* — See current mounts  
*`cat /etc/fstab`* — Check permanent mount configuration  

---

# 🛑 8. Investigate Disk I/O Problems

Look for processes causing heavy disk usage.

**Commands:**  
*`iostat -xz 1`* — Live disk I/O metrics  
*`iotop`* — Show processes using disk heavily  
*`vmstat 1`* — General system performance  

