# Week 2 — Practical Cybersecurity Assignment

## Student Info
- Name:Rushikesh Pawar
- Repository:Cyart-red-teaming
- Week: 2
- Deadline: Friday 4:30 PM

---

## Overview
This repository contains practical cybersecurity tasks covering 
Threat Hunting, Malware Analysis, Vulnerability Management, 
Incident Response, Network Defense, Risk Assessment, and a 
full Capstone simulation.

---

## Repository Structure
Week-2/
├── Task-1-ThreatHunting/
│   ├── notes.md
│   ├── powershell_detect.yml
│   └── screenshots/
├── Task-2-MalwareAnalysis/
│   ├── notes.md
│   ├── output.txt
│   └── screenshots/
├── Task-3-VulnManagement/
│   ├── notes.md
│   ├── report.xml
│   └── screenshots/
├── Task-4-IRSimulation/
│   └── notes.md
├── Task-5-NetworkDefense/
│   ├── notes.md
│   ├── local.rules
│   └── screenshots/
├── Task-6-RiskALE/
│   ├── notes.md
│   └── ale-calculation.pdf
├── Task-7-IRReport/
│   ├── notes.md
│   ├── IR-Report-2025-001.pdf
│   └── IR-Flowchart.png
└── Task-8-Capstone/
├── notes.md
├── capstone-report.md
└── screenshots/

---

## Tasks Summary

| Task | Description | Status | Tools Used |
|------|-------------|--------|------------|
| Task 1 | Threat Hunting | ✅ Complete | Sigma Rules, Event Viewer, PowerShell |
| Task 2 | Malware Analysis | ✅ Complete | REMnux, Hybrid Analysis |
| Task 3 | Vulnerability Management | ✅ Complete | OpenVAS, Metasploitable2 |
| Task 4 | IR Simulation | ⚠️ Documented | MITRE ATT&CK Framework |
| Task 5 | Network Defense | ✅ Complete | Suricata 8.0.5 |
| Task 6 | Risk ALE | ✅ Complete | Google Sheets |
| Task 7 | IR Report | ✅ Complete | Google Docs, draw.io |
| Task 8 | Capstone | ✅ Complete | Metasploit, Kali Linux |

---

## Task Details

### Task 1 — Threat Hunting
- Sigma rule created for PowerShell detection
- Event ID 4688 captured via Windows Event Viewer
- MITRE Technique: T1059.001

### Task 2 — Malware Analysis
- Static analysis performed on calc.exe using REMnux
- Dynamic analysis via Hybrid Analysis
- Verdict: Clean file — no malicious behavior

### Task 3 — Vulnerability Management
- Metasploitable2 scanned using OpenVAS
- Top vulnerability: VSFTPD 2.3.4 Backdoor (CVSS 7.5)
- Results documented in vulnerability table

### Task 4 — IR Simulation
- Caldera setup attempted — network restriction faced
- Attack path documented using MITRE ATT&CK framework
- Techniques mapped: T1566, T1059, T1053, T1041

### Task 5 — Network Defense
- Suricata installed and configured on Kali Linux
- Custom rules created for malicious IP blocking
- Alerts mapped to MITRE ATT&CK techniques

### Task 6 — Risk ALE
- ALE calculated: SLE ($10,000) × ARO (0.2) = $2,000
- 5×5 Risk Matrix created with color coding
- Ransomware scenario: Likelihood 2, Impact 5 = Score 10

### Task 7 — IR Report
- Phishing incident report written using SANS template
- IR Flowchart created using draw.io
- Covers: Detection → Containment → Eradication → Recovery

### Task 8 — Capstone
- VSFTPD backdoor exploited via Metasploit
- Root shell obtained on Metasploitable2
- Full IR cycle documented and reported

---

## Key Learnings
- Applied STRIDE threat modeling practically
- Mapped real attacks to MITRE ATT&CK techniques
- Performed actual vulnerability exploitation in lab
- Followed complete Incident Response lifecycle
- Calculated quantitative risk using ALE formula

---

## Tools Used
| Tool | Purpose |
|------|---------|
| Sigma Rules | Threat detection rules |
| Windows Event Viewer | Log analysis |
| REMnux | Malware static analysis |
| Hybrid Analysis | Dynamic malware analysis |
| OpenVAS | Vulnerability scanning |
| Suricata | Network IDS |
| Metasploit | Attack simulation |
| Google Sheets | Risk calculation |
| draw.io | Flowchart creation |
| MITRE ATT&CK | Technique mapping |

---

## References
- [MITRE ATT&CK Framework](https://attack.mitre.org)
- [SANS Incident Response](https://www.sans.org)
- [OpenVAS Documentation](https://www.openvas.org)
- [Suricata Documentation](https://suricata.io)
- [Sigma Rules](https://github.com/SigmaHQ/sigma)
