# AWS Cloud Security Lab — IAM, S3, EC2 & VPC

## Overview
A hands-on AWS cloud security project built from scratch 
as an AppSec student, focusing on security best practices 
and real world cloud architecture.

## Services Used
| Service | Purpose |
|---------|---------|
| **IAM** | Users, roles and policies |
| **S3** | Private secure file storage |
| **EC2** | Ubuntu virtual web server |
| **VPC** | Custom private network |
| **Nginx** | Web server on EC2 |
| **AWS CLI** | S3 access from EC2 |

## Security Configurations

### IAM
- [x] Root account not used for daily work
- [x] IAM user created with least privilege
- [x] IAM role attached to EC2 (no access keys)
- [x] No hardcoded credentials anywhere

### S3
- [x] Block public access enabled
- [x] Server side encryption (SSE-S3)
- [x] Versioning enabled
- [x] Access logging enabled
- [x] Bucket owner enforced (ACLs disabled)

### EC2
- [x] Port 22 restricted to my IP only
- [x] Port 80 closed after testing
- [x] Key pair authentication (no passwords)
- [x] IAM role used instead of credentials

### VPC
- [x] Custom VPC with CIDR 10.0.0.0/16
- [x] Public and private subnets
- [x] Internet Gateway configured
- [x] Route tables configured
- [x] Security groups with least privilege
- [x] Outbound rules restricted

## Setup Steps

### 1. IAM Setup
```bash
# Created IAM user with AdministratorAccess
# Created IAM role for EC2 with S3ReadOnlyAccess
# Attached role to EC2 instance
```

### 2. S3 Setup
```bash
# Created private bucket
# Enabled versioning and encryption
# Enabled access logging
# Uploaded index.html
```

### 3. VPC Setup
```bash
# Created custom VPC (10.0.0.0/16)
# Created public subnet (10.0.0.0/20)
# Created private subnet (10.0.128.0/20)
# Configured Internet Gateway
# Configured route tables
# Created appsec-sg security group
```

### 4. EC2 Setup
```bash
# Launched Ubuntu t3.micro in appsec-vpc public subnet
# Configured security group (port 22 my IP only)
# Attached IAM role ec2-s3-read-role
# SSHed in from Windows PowerShell
ssh -i $HOME\Downloads\aws-lab-key.pem ubuntu@YOUR.PUBLIC.IP
```

### 5. Install Nginx and AWS CLI
```bash
sudo apt -o Acquire::ForceIPv4=true update -y
sudo apt -o Acquire::ForceIPv4=true install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo apt -o Acquire::ForceIPv4=true install awscli -y
```

### 6. Pull index.html from S3
```bash
sudo aws s3 cp s3://your-bucket-name/index.html /var/www/html/
```

## Key AppSec Lessons Learned
1. Never use root account for daily work
2. Always restrict SSH to your IP only
3. Use IAM roles not hardcoded credentials
4. Block public access on S3 buckets
5. Close unused ports immediately
6. Every open port is a potential attack surface
7. Outbound rules matter as much as inbound
8. Always check VPC and subnet configurations

## Common Errors & Fixes
| Error | Cause | Fix |
|-------|-------|-----|
| `iam:CreateUser not authorized` | Wrong user logged in | Log in as root |
| `Permission denied .pem` | Wrong file permissions | Run icacls command |
| `Connection timed out SSH` | IP changed after restart | Update security group My IP |
| `Network unreachable` | Missing outbound rules | Add all traffic outbound rule |
| `apt update failed` | IPv6 blocked | Use `-o Acquire::ForceIPv4=true` |

## Screenshots 
> Add your screenshots here
- [ ] VPC architecture
- [ ] S3 bucket permissions
- [ ] Security group rules
- [ ] IAM role configuration
- [ ] Website running in browser



