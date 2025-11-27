🌐 Website / Service Not Loading
Linux Troubleshooting Cheat Sheet (Quick Practical Guide)

This guide helps you diagnose why a website is not loading, a service is unreachable, or network connectivity is failing from a Linux system.

1️⃣ Step 1 — Check Basic Network Connectivity
Check if the system has an IP
ip a

Check the default gateway
ip route

Ping the gateway
ping -c 4 <gateway_IP>

Ping the internet
ping -c 4 8.8.8.8


If 8.8.8.8 works but websites do not → DNS issue.

2️⃣ Step 2 — DNS Troubleshooting
Check if DNS can resolve the domain
dig google.com


or

nslookup google.com

Check DNS server configuration
cat /etc/resolv.conf

3️⃣ Step 3 — Check if Website's Server is Reachable
Test if remote port is open
nc -zv <IP> <port>


Example:

nc -zv 142.250.179.14 443

Check local listening ports
ss -tulnp

Test HTTP/HTTPS response headers
curl -I http://<domain>

4️⃣ Step 4 — Trace the Connection Path
Identify where the connection is failing
traceroute <domain>

5️⃣ Step 5 — Check Firewall Issues
Ubuntu/Debian firewall
sudo ufw status

Firewalld
sudo firewall-cmd --list-all

Raw iptables rules
sudo iptables -L -n -v

6️⃣ Step 6 — Check System & Service Logs
System logs
journalctl -xe

Network or connection-related errors
dmesg | grep -i network

7️⃣ Step 7 — Check the Network Interface
Check NIC status
ip link show

Hardware link status
ethtool eth0

8️⃣ Optional: Capture Live Traffic
See packets flowing (useful for unreachable services)
sudo tcpdump -i eth0 port 80
