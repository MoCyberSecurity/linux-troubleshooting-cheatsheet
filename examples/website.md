# 🌐 Website / Service Not Loading  
### Linux Troubleshooting Cheat Sheet — Practical Investigation Steps

This guide helps diagnose why a **website isn’t loading**, a **service is unreachable**, or **network connectivity is failing** from a Linux machine.

---

# 🚀 1. Check Basic Connectivity

### 🔎 Does the system have an IP?
```bash
ip a

🔎 Check the default gateway
ip route

🔎 Ping the gateway
ping -c 4 <gateway_IP>

🔎 Ping the internet (Google DNS)
ping -c 4 8.8.8.8


✅ If 8.8.8.8 works but websites don’t → DNS problem

# 🧭 2. DNS Troubleshooting
🔍 Resolve a domain name
dig google.com

🔍 Alternative DNS lookup
nslookup google.com

🔍 Check DNS configuration
cat /etc/resolv.conf


⚠️ Incorrect or empty /etc/resolv.conf = broken DNS configuration

🌍 3. Check Remote Server Reachability
🔌 Test if a remote port is open
nc -zv <IP> <port>

🔌 Check local listening services
ss -tulnp

🔌 Check web server headers
curl -I http://<domain>


Example problems: 301, 403, 404, SSL errors

🛰️ 4. Trace the Path (Find Where It Breaks)
🧭 Trace route to the destination
traceroute <domain>

🧭 Alternative (TCP-based)
tcptraceroute <domain> 443


Helps identify where the connection fails (ISP, network hop, target server)

🔥 5. Firewall Checks
UFW (Ubuntu/Debian)
sudo ufw status

Firewalld
sudo firewall-cmd --list-all

Raw iptables rules
sudo iptables -L -n -v


❗ Common issue: inbound/outbound traffic blocked

📜 6. Log Analysis
System logs
journalctl -xe

Network-related kernel messages
dmesg | grep -i network

Web server logs (example: nginx)
sudo tail -f /var/log/nginx/error.log


Useful for SSL failures, timeouts, DNS errors, blocked packets

🧩 7. Network Interface Health
NIC status
ip link show

Hardware link activity
ethtool eth0

Check interface throughput
sar -n DEV 1


Detects down interfaces, duplex mismatch, cable issues

🛰️ 8. Packet Capture (Advanced)
Capture traffic for port 80 (HTTP)
sudo tcpdump -i eth0 port 80

Capture traffic to specific host
sudo tcpdump -i eth0 host <IP>

Write capture to file for Wireshark
sudo tcpdump -i eth0 -w capture.pcap


Ideal for deep debugging: dropped packets, resets, DNS failures, TLS errors
