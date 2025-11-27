# 🌐 Website / Service Not Loading  
### Linux Troubleshooting Cheat Sheet — Practical Investigation Steps

This guide helps diagnose why a **website isn’t loading**, a **service is unreachable**, or **network connectivity is failing** from a Linux machine.

---

# 🚀 1. Check Basic Connectivity

### 🔎 Does the system have an IP?
*`ip a`*

### 🔎 Check the default gateway
*`ip route`*

### 🔎 Ping the gateway
*`ping -c 4 <gateway_IP>`*

### 🔎 Ping the internet (Google DNS)
*`ping -c 4 8.8.8.8`*

> ✅ If 8.8.8.8 works but websites don’t → **DNS problem**

---

# 🧭 2. DNS Troubleshooting

### 🔍 Resolve a domain name
*`dig google.com`*

### 🔍 Alternative DNS lookup
*`nslookup google.com`*

### 🔍 Check DNS configuration
*`cat /etc/resolv.conf`*

> ⚠️ Incorrect or empty `/etc/resolv.conf` = **broken DNS**

---

# 🌍 3. Check Remote Server Reachability

### 🔌 Test if a remote port is open
*`nc -zv <IP> <port>`*

### 🔌 Check local listening services
*`ss -tulnp`*

### 🔌 Check HTTP/HTTPS response headers
*`curl -I http://<domain>`*

> Helps detect **redirects, SSL issues, server errors**

---

# 🛰️ 4. Trace the Path (Find Where It Breaks)

### 🧭 Standard traceroute
*`traceroute <domain>`*

### 🧭 TCP-based traceroute
*`tcptraceroute <domain> 443`*

> Reveals **where** the connection fails (ISP, firewall, server)

---

# 🔥 5. Firewall Checks

### UFW (Ubuntu/Debian)
*`sudo ufw status`*

### Firewalld (RHEL/CentOS)
*`sudo firewall-cmd --list-all`*

### Raw iptables rules
*`sudo iptables -L -n -v`*

> ❗ Common issue: blocked outbound HTTP/HTTPS

---

# 📜 6. Log Analysis

### System logs
*`journalctl -xe`*

### Kernel logs (network-related)
*`dmesg | grep -i network`*

### Web server logs (example: nginx)
*`sudo tail -f /var/log/nginx/error.log`*

> Useful for **DNS failures, SSL issues, timeouts**

---

# 🧩 7. Network Interface Health

### View interface status
*`ip link show`*

### Check hardware link state
*`ethtool eth0`*

### Check network usage
*`sar -n DEV 1`*

> Helps diagnose **down interfaces, duplex mismatch, cable faults**

---

# 🛰️ 8. Packet Capture (Advanced)

### Capture HTTP traffic
*`sudo tcpdump -i eth0 port 80`*

### Capture traffic to/from specific host
*`sudo tcpdump -i eth0 host <IP>`*

### Save capture for Wireshark
*`sudo tcpdump -i eth0 -w capture.pcap`*

> Essential for deep analysis of **TLS errors, resets, dropped packets**

---

# ✔️ Summary of Issues You Can Diagnose

- DNS issues  
- Firewall blocks  
- Routing problems  
- Remote service down  
- SSL errors  
- Network hop failures  
- Packet drops  
- NIC/cable problems  
