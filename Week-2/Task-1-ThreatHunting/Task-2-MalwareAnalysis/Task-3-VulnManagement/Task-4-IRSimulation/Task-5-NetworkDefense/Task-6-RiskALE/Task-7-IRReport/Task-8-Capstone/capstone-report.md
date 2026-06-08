Task 8 — Capstone: Full Incident Response Cycle

1. Attack Simulation
- Tool: Metasploit Framework
- Target: Metasploitable2 (192.168.1.3)
- Attacker: Kali Linux (192.168.1.4)
- Exploit: vsftpd_234_backdoor
- MITRE Technique: T1190 (Exploit Public-Facing Application)
- Result: Root shell obtained successfully

2. Detection
| Timestamp           | Source IP   | Alert Description   | MITRE Technique |
|---------------------|-------------|---------------------|-----------------|
| 2026-06-03 11:11:44 | 192.168.1.4 | VSFTPD exploit used | T1190           |
| 2026-06-03 11:11:44 | 192.168.1.4 | Root shell obtained | T1068           |

3. Containment
Attacker IP blocked using iptables:
 iptables -A INPUT -s 192.168.1.4 -j DROP
 iptables -A OUTPUT -d 192.168.1.4 -j DROP

Metasploitable VM network isolated immediately.

4. Eradication
- VSFTPD service disabled
- Backdoor port 6200 closed
- System scanned for persistence

5. Recovery
- Clean snapshot restored
- All services verified
- Monitoring enabled

6. Recommendations
1. Patch VSFTPD immediately
2. Disable unused FTP service
3. Implement network segmentation
4. Schedule regular vulnerability scans
5. Deploy IDS/IPS (Suricata)

7. Lessons Learned
- VSFTPD 2.3.4 backdoor is a known critical vulnerability
- Unpatched systems are easy targets
- Network monitoring essential for early detection
