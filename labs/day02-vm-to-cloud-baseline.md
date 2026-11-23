# Day 02: On-Premises Virtualization to Cloud Security Baseline

## 1. Lab Architecture Overview
- **Hypervisor Used:** VMware Workstation Pro
- **Virtual Machines Deployed:** Windows Server 2019, Windows Server 2022, Windows Server 2025, Linux & Windows Clients
- **Network Mode:** Host-Only , Internal Virtual Switch ,  NAT

## 2. How On-Premises Infrastructure Maps to AWS Cloud
| On-Prem / Hypervisor Concept | Cloud Equivalent (AWS) | Security Purpose |
| :--- | :--- | :--- |
| Virtual Machine (VM) | Amazon EC2 Instance | Isolated compute workload |
| Virtual Switch / Subnet | Amazon VPC & Subnets | Network segmentation |
| Host / Guest Firewall Rules | Security Groups & NACLs | Controlling inbound & outbound traffic |
| Local Admin / Active Directory | AWS IAM (Users, Roles, Policies) | Identity & least-privilege access |

## 3. Top 3 Infrastructure Security Risks & Hardening Controls
1. **Risk: Exposed Management Ports (RDP 3389 / SSH 22)**
   - **Impact:** Attackers continuously scan and brute-force publicly exposed remote management interfaces.
   - **Hardening Control:** Restrict management ports strictly to trusted admin IP ranges or use AWS Systems Manager (SSM) Session Manager instead of opening public ports.
2. **Risk: Over-Privileged Administrative Accounts**
   - **Impact:** Compromising a daily-use admin account gives an attacker full control over the hypervisor, domain, or cloud tenant.
   - **Hardening Control:** Enforce **Least Privilege**—separate daily user accounts from admin roles and enforce MFA.
3. **Risk: Unnecessary Running Services & Weak File Permissions**
   - **Impact:** Default open ports or loose directory permissions allow privilege escalation and lateral movement.
   - **Hardening Control:** Disable unused services, enforce host firewalls (`ufw` / Windows Firewall), and lock down sensitive config file permissions.
