# 🏦 Nile Bank — Enterprise IT Infrastructure Lab

A hands-on enterprise infrastructure lab designed to practice Windows Server administration, networking, identity management, Linux administration, monitoring, backup, and disaster recovery concepts in a controlled virtual environment.

## 🎯 Project Objectives

- Build practical enterprise IT infrastructure administration skills.
- Practice Active Directory Domain Services (AD DS), DNS, DHCP, and Group Policy.
- Configure and troubleshoot Windows Server and Linux systems.
- Explore centralized monitoring using Zabbix.
- Document infrastructure architecture, configuration, troubleshooting, and testing.
- Develop practical skills relevant to System Administrator, IT Infrastructure Engineer, and Cloud Engineer roles.

## 🏗️ Lab Environment

| Component | Technology |
|---|---|
| Virtualization | Microsoft Hyper-V |
| Host operating system | Windows 11 |
| Server environment | Windows Server 2025 Evaluation |
| Linux environment | Linux Server |
| Network | Isolated Hyper-V Internal virtual switch |
| Monitoring | Zabbix |
| Directory services | Active Directory Domain Services |
| Infrastructure services | DNS, DHCP, file and print services |
| Documentation | Markdown, diagrams, configuration notes, and test evidence |

*The table describes the lab environment and planned scope. Individual services and tests should be marked as completed only after they have been configured and verified.*

## 🌐 Network Design

The documented design uses the following example addressing scheme:

| Resource | Example IP address |
|---|---|
| Lab subnet | `10.10.30.0/24` |
| DC01 | `10.10.30.10` |
| DHCP server | `10.10.30.12` |

These are documented design values; verify them against the current lab configuration before treating them as actual running settings.

## 🔧 Key Learning Areas

- Active Directory domain design, users, groups, and organizational units
- DNS resolution and troubleshooting
- DHCP scopes and client addressing
- Group Policy configuration and validation
- File server shares and NTFS permissions
- Print server administration
- Linux administration and networking
- Zabbix monitoring and troubleshooting
- Backup, recovery, and domain controller failover testing
- PowerShell-based administration and automation

## 🧪 Testing and Troubleshooting

The project documentation covers infrastructure validation, connectivity troubleshooting, service health checks, monitoring, and recovery exercises.

Test results will be documented using actual command output, screenshots, timestamps, and observations. Expected results will not be presented as completed tests.

## 🔐 Security and Documentation Practices

- Keep passwords, private keys, recovery secrets, and other credentials out of the repository.
- Sanitize screenshots and command output before publishing.
- Use fictional lab identities and IP addresses in public documentation.
- Review files before committing or changing repository visibility.
- Distinguish implemented features from planned improvements.

## ☁️ Future Improvements

Potential extensions include infrastructure automation, expanded monitoring, improved backup and disaster recovery, and a separately implemented Azure integration.

Cloud services will be documented as implemented only after they have been configured and tested.

## 📁 Project Documentation

The repository will organize architecture, network configuration, Active Directory, DNS, DHCP, Group Policy, file and print services, Linux, monitoring, backup and disaster recovery, security, scripts, troubleshooting, and supporting evidence.

## 💼 Career Relevance

This project supports practical learning for roles such as:

- IT Support Engineer
- System Administrator
- IT Infrastructure Engineer
- Junior Cloud Engineer

**Project type:** Personal hands-on lab  
**Environment:** Virtualized, non-production  
**Project name:** Nile Bank — Enterprise IT Infrastructure Lab
