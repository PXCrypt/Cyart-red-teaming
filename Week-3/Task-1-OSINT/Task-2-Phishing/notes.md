# Task 2 - Phishing Simulation

## Tools Used
- Gophish
- Evilginx2

## Campaign Setup
- Cloned login page with Evilginx2
- Sent phishing link via Gophish campaign
- Tested on Windows 10 VM

## Credential Harvest
| Timestamp           | IP Address  | Username/Password      | Risk | Notes              |
|---------------------|-------------|------------------------|------|--------------------|
| 2026-06-06 05:12:35 | 192.168.1.6 | me7@gmail.com/pass123  | High | Successful capture |

## Summary
Evilginx2 generated phishing link for academy.example.com.
Gophish campaign launched. Windows VM victim opened
link and submitted credentials. Successfully captured
via Evilginx2 sessions.
