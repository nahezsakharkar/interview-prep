---
title: "Linux Commands Cheat Sheet"
tags: ["devops","linux","cli"]
difficulty: easy
status: revised
last_reviewed: 2026-10-02
---

# Linux Commands Cheat Sheet

## 1. File and Directory Management
| Command | Purpose | Example |
| :--- | :--- | :--- |
| `ls -lah` | List all files with human-readable sizes | `ls -lah /var/log` |
| `find` | Search for files by name, date, or size | `find /etc -name "*.conf"` |
| `grep -ri` | Search for text recursively in files | `grep -ri "ERROR" /var/log` |
| `chmod` | Change file permissions | `chmod 600 ~/.ssh/id_rsa` |
| `chown` | Change file owner/group | `chown nginx:nginx /var/www/html` |
| `du -sh` | Show total size of a directory | `du -sh /home/user/data` |

## 2. System Monitoring and Process Management
| Command | Purpose | Example |
| :--- | :--- | :--- |
| `top` / `htop` | Real-time system resource monitor | `htop` |
| `ps aux` | Snapshot of all running processes | `ps aux | grep java` |
| `kill -9` | Forcefully terminate a process | `kill -9 1234` |
| `df -h` | Show disk space usage | `df -h` |
| `free -m` | Show memory usage in MB | `free -m` |
| `ss -tulpn` | List listening ports and processes | `ss -tulpn | grep 8080` |

## 3. Networking and Logs
| Command | Purpose | Example |
| :--- | :--- | :--- |
| `curl -I` | Fetch HTTP headers only | `curl -I https://google.com` |
| `netstat` | Network connection statistics | `netstat -an` |
| `tail -f` | Follow a file in real-time (logs) | `tail -f /var/log/syslog` |
| `journalctl -u` | View logs for a specific systemd unit | `journalctl -u nginx -f` |
| `systemctl` | Manage systemd services | `systemctl restart nginx` |

## 4. Text Processing (The "Power Trio")

### `grep` (Global Regular Expression Print)
Used to filter lines.
- `grep "ERROR" app.log`: Find lines containing "ERROR".
- `grep -v "INFO" app.log`: Find lines NOT containing "INFO".

### `awk` (Pattern Scanning and Processing)
Used to extract columns.
- `awk '{print $1}' access.log`: Print the first column (usually the IP address) of every line.
- `awk '$9 == 404 {print $1}' access.log`: Print the IP of every request that resulted in a 404.

### `sed` (Stream Editor)
Used to transform text.
- `sed -i 's/localhost/api.prod.com/g' config.yml`: Replace all occurrences of "localhost" with "api.prod.com" in the file.

## Working Code Example: Log Analysis One-Liner

This command finds the top 5 IP addresses that caused 500 errors in an Nginx access log.

```bash
cat /var/log/nginx/access.log | grep " 500 " | awk '{print $1}' | sort | uniq -c | sort -rn | head -n 5
```

**Breakdown**:
1. `cat`: Read the file.
2. `grep " 500 "`: Filter for lines with a 500 status code.
3. `awk '{print $1}'`: Extract only the IP address (first column).
4. `sort`: Sort IPs so identical ones are adjacent.
5. `uniq -c`: Count occurrences of each unique IP.
6. `sort -rn`: Sort by count (`-n` numeric, `-r` reverse).
7. `head -n 5`: Take the top 5 results.

## Interview questions

### Q1: How do you find a process running on port 8080 and kill it?
**Model answer**: First, I use `ss -tulpn | grep 8080` or `lsof -i :8080` to find the Process ID (PID). Then, I use `kill -9 <PID>` to terminate the process.

### Q2: What is the difference between `soft link` (symbolic) and `hard link`?
**Model answer**: A hard link is a direct pointer to the inode of the file; it's indistinguishable from the original file. A soft link is a pointer to the file path; if the original file is moved or deleted, the soft link becomes "broken".

### Q3: How do you search for all files larger than 100MB in `/var`?
**Model answer**: `find /var -type f -size +100M`.

### Q4: How do you monitor a log file in real-time while filtering for a specific keyword?
**Model answer**: `tail -f /var/log/app.log | grep "CRITICAL"`.

### Q5: What does `chmod 400` do to a file?
**Model answer**: It sets the permissions so that only the owner can read the file, and no one (including the owner) can write or execute it. This is commonly used for private SSH keys.

## Related notes

- [Ansible Automation](../08-devops/ansible-automation.md)
- [Jenkins](../08-devops/jenkins.md)
- [Kubernetes Basics](../08-devops/kubernetes-basics.md)
