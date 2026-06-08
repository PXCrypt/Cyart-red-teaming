# Task 1 — Threat Hunting with Open-Source Tools

## Tools Used
- Sigma Rules
- Windows Event Viewer
- PowerShell

## Steps Performed
1. Sigma rule created for PowerShell detection
2. PowerShell command executed: `powershell -Command "Write-Host Test"`
3. Event ID 4688 captured in Event Viewer

## Files
- powershell_detect.yml — Sigma rule
- screenshots/ — Event Viewer proof

## MITRE Mapping
- T1059.001 — PowerShell execution
