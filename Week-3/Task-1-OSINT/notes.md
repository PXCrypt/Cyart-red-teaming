# Task 1 - OSINT & Recon

## Tools Used
- Recon-ng
- Shodan

## Subdomain Enumeration
| Subdomain       | IP Address    | Notes       |
|-----------------|---------------|-------------|
| www.example.com | 104.20.23.154 | Web server  |
| example.com     | 93.184.216.34 | Main domain |
| *.example.com   | 93.184.216.34 | Wildcard    |

## Shodan Query: apache country:US
| Host IP       | Location   | Details              |
|---------------|------------|----------------------|
| 47.90.149.238 | US, Ashburn| Apache/2.2.15 CentOS |
| 51.81.232.226 | US,Portland| Apache, WordPress    |
| 3.168.86.55   | US,San Jose| Apache, Cloudfront   |

## Summary
143 subdomains found via certificate_transparency module.
Three Apache servers found in US via Shodan.
