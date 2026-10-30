# Architecture Design Decisions

## 1. Project Overview

The Nile Bank lab is a personal, non-production environment for learning enterprise IT infrastructure administration and troubleshooting.

The lab uses Microsoft Hyper-V to host virtual machines running Windows Server and Linux. Its design focuses on identity management, network services, infrastructure monitoring, and operational documentation.

## 2. Virtualization Platform

**Technology:** Microsoft Hyper-V on a Windows 11 host.

### Rationale
- Run multiple server workloads on one physical computer.
- Practice virtual machine provisioning and resource allocation.
- Test infrastructure changes in a controlled environment.
- Learn troubleshooting and recovery without affecting a production network.

## 3. Network Isolation

**Planned lab network:** `10.10.30.0/24`  
**Virtual switch:** Hyper-V Internal

The Internal virtual switch provides connectivity between the Windows host and attached virtual machines. It does not, by itself, provide internet access to those machines.

Any internet connectivity must be configured and tested separately.

### Rationale
- Keep lab traffic separate from the physical network by default.
- Practice IP addressing, DNS, DHCP, and connectivity troubleshooting.
- Reduce the risk of unintended changes to other networks.

## 4. Identity and Infrastructure Services

The lab design includes the following service areas:

- Active Directory Domain Services for centralized identity management.
- DNS for name resolution.
- DHCP for automatic client IP configuration.
- File and print services for resource-sharing exercises.
- Linux administration and network services.
- Zabbix for infrastructure monitoring.

Each service should have its own configuration notes and validation evidence.

## 5. Monitoring

Zabbix is used as the monitoring platform for learning host monitoring, agent configuration, availability checks, and alert troubleshooting.

Document only hosts, metrics, triggers, and alerts that have been verified in the running environment.

## 6. Resource Constraints

The physical host has a Ryzen 5 2600X processor and 16 GB of RAM.

Virtual machine CPU and memory allocations must be balanced against the host's available resources. Running every VM simultaneously may affect performance, so resource usage should be monitored during testing.

## 7. Security and Change Management

- Use fictional identities and lab-only credentials.
- Never commit passwords, private keys, or recovery secrets.
- Test configuration changes in the isolated lab.
- Record the change, expected outcome, actual result, and rollback steps for significant tests.
- Keep planned features separate from completed and validated implementations.

## 8. Current Status and Future Work

This document describes the architectural rationale, not proof that every planned service is deployed.

The implementation status of each server and service should be recorded separately. Potential future work includes improved backup and disaster recovery, automation, expanded monitoring, and an Azure integration.

Cloud integration must not be described as implemented until it has been built and tested.

## 9. Project Scope

This is an educational home lab. It does not represent a real bank's production infrastructure, security controls, or regulatory compliance.
