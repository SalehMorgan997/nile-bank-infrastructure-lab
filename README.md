# Nile Bank — Enterprise Infrastructure Lab

## Project Overview

Nile Bank is a personal enterprise IT infrastructure lab designed to simulate selected services commonly found in a corporate banking environment.

The project provides hands-on practice in Windows Server administration, virtualization, network services, infrastructure monitoring, troubleshooting, and recovery planning.

**Project type:** Personal technical project / home lab  
**Status:** In progress  
**Environment:** Isolated Hyper-V virtual lab

## Objectives

- Deploy and administer Windows Server virtual machines.
- Configure Active Directory Domain Services and DNS.
- Practice DHCP and Group Policy administration.
- Develop file and print server infrastructure.
- Integrate Linux servers into the lab.
- Monitor infrastructure using Zabbix.
- Document troubleshooting, backup, and recovery procedures.

## Technology Stack

- Microsoft Hyper-V
- Windows 11 host
- Windows Server 2025 Evaluation
- Active Directory Domain Services (AD DS)
- DNS and DHCP
- Group Policy
- Linux Server
- Zabbix
- TCP/IP and virtual networking
- PowerShell

## Architecture

See [`architecture/network-design.md`](architecture/network-design.md).

## Implementation Guides

- Active Directory and DNS: `implementation-guides/active-directory.md`
- Zabbix monitoring: `implementation-guides/zabbix.md`

## Troubleshooting

Documented incidents, diagnostic commands, root causes, and verified resolutions are maintained in `troubleshooting/troubleshooting-log.md`.

## Backup and Recovery

Recovery plans and test results are maintained in `recovery/disaster-recovery.md`.

## Project Evidence

Screenshots and sanitized diagrams are stored in the `screenshots/` and `architecture/` directories.

## Security and Scope

This is a personal learning environment, not a production banking system.

All documentation is sanitized for public release. No credentials, private keys, license keys, personal information, or confidential employer data should be published.

All recovery and failover exercises are performed in the isolated lab.

## Learning Outcomes

- Windows Server and identity administration
- Virtualization and network troubleshooting
- Linux infrastructure monitoring
- Technical documentation and recovery planning

*This documentation describes only features that have actually been implemented or tested. Planned features are identified separately.*
