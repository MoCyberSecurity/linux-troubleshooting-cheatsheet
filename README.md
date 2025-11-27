# linux-troubleshooting-cheatsheet
A beginner-friendly guide to Linux commands for troubleshooting systems, networking, and processes
# Linux Troubleshooting Commands for Beginners

## System & Process Checks
- `pwd` – print current working directory
- `ls -la` – list files including hidden and permissions
- `top` – monitor CPU, memory, and processes
- `dmesg | tail` – view recent system/kernel messages
- `lsof -i -n -P` – check open network connections and files

## Networking & Connectivity
- `ip addr` / `ip a` – list network interfaces and IP addresses
- `ping <host>` – test connectivity
- `traceroute <host>` – see path to remote host
- `nslookup <domain>` / `dig <domain>` – DNS resolution
- `ss` – view listening ports and active connections
- `curl <URL>` – test HTTP connectivity

## Permissions, File & Disk Checks
- `ls -l <file>` – check permissions and ownership
- `grep -R "pattern" /path` – search for text in files
- `diff file1 file2` – compare files
- `df -h` – check disk usage
- `lsblk` – view disks and partitions

## Example Troubleshooting Workflow
1. Check system load: `top`
2. Verify network: `ip addr`, `ping <host>`
3. Check services: `ss`, `curl <service>`
4. Inspect logs: `grep -R "error" /var/log/`
5. Check files and permissions: `ls -l /path`
6. Check disk usage: `df -h`, `lsblk`


## Examples

- [Website Not Loading](examples/website.md)
- [Service Not Starting](examples/service.md)
- [Disk Full / Filesystem Issue](examples/disk.md)

