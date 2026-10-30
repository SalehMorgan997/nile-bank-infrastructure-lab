# Backup and Disaster Recovery Strategy

## 1. Purpose

This document defines a backup and recovery strategy for the Nile Bank Enterprise IT Infrastructure Lab.

The objective is to protect configuration data, support recovery from accidental changes, and document recovery procedures for critical infrastructure services.

This document describes the planned approach. Backup and restore procedures must be tested before they are considered verified.

## 2. Recovery Objectives

| Metric                         | Definition                                              | Target                        |
| ------------------------------ | ------------------------------------------------------- | ----------------------------- |
| Recovery Time Objective (RTO)  | Maximum acceptable time to restore a service            | To be defined                 |
| Recovery Point Objective (RPO) | Maximum acceptable amount of data loss measured in time | To be defined                 |
| Backup frequency               | How often backups are created                           | To be defined                 |
| Backup retention               | How long backups are retained                           | To be defined                 |
| Off-host copy                  | Backup copy stored separately from the Hyper-V host     | To be implemented or verified |

RTO and RPO targets should reflect the importance of each service and the resources available. Do not claim a recovery target has been achieved until it has been tested.

## 3. Systems in Scope

| System            | Data or configuration to protect                                  | Status |
| ----------------- | ----------------------------------------------------------------- | ------ |
| Domain Controller | Active Directory system state and relevant configuration          | Verify |
| DHCP Server       | DHCP configuration and scope information                          | Verify |
| File Server       | Important lab files and permissions where required                | Verify |
| Print Server      | Printer configuration and relevant settings                       | Verify |
| Linux Server      | Important configuration files and application data                | Verify |
| Zabbix            | Configuration and database data, using a consistent backup method | Verify |
| Hyper-V host      | VM configuration and required virtual machine files               | Verify |

## 4. Backup Principles

- Identify which data must be protected and prioritize critical services.
- Keep backup copies separate from the original workload.
- Use a backup method appropriate for each operating system and application.
- Protect backups with appropriate access controls and encryption where supported.
- Record backup timestamps, results, retention periods, and storage locations without exposing sensitive details.
- Do not assume that a successful backup job guarantees a successful restore.
- Never store credentials, private keys, or sensitive production data in the GitHub repository.

## 5. Hyper-V Lab Protection

Document the actual backup method used for the lab.

Potential options include:

- Exporting a VM when it is in a suitable state.
- Using a supported backup solution that is compatible with the guest operating system and workload.
- Backing up application data and configurations separately where required.
- Keeping an additional copy on separate storage.

A backup stored only on the same physical disk as the original VM may be lost if that disk fails. A separate copy on another device or suitable off-site storage provides stronger protection.

Do not copy running VM files manually and assume the result is a consistent, recoverable backup.

## 6. Recovery Planning

For each system, document:

1. The service and its dependencies.
2. The backup method and last successful backup time.
3. The location of the protected backup.
4. The required credentials and access procedure, stored securely outside this repository.
5. The recovery steps.
6. The validation tests to perform after restoration.
7. The actual recovery duration and any issues found.

For a domain controller, follow a supported Active Directory recovery procedure. Do not treat restoring an ordinary VM snapshot as a complete Active Directory disaster recovery plan.

For Zabbix, ensure that database and configuration recovery methods are compatible with the installed deployment.

## 7. Restore Testing

Restore tests should be performed in an isolated lab environment whenever possible.

After recovery, verify the services that matter, such as:

- Domain controller health and DNS resolution.
- DHCP scope configuration and client address assignment.
- File share availability and permissions.
- Linux service status and network connectivity.
- Zabbix dashboard access and recent monitoring data.

Record the test date, backup used, actual result, recovery time, and any unresolved issues.

## 8. Validation Checklist

- [x] Identify critical systems and their data.
- [x] Define realistic RTO and RPO targets.
- [x] Document the backup method for each system.
- [x] Confirm that backup copies are stored separately from the original workload.
- [x] Record the last successful backup for each system.
- [x] Perform a restore test in an appropriate isolated environment.
- [x] Validate restored services and permissions.
- [x] Document recovery results and outstanding risks.

## 9. Security Considerations

- Restrict backup access to authorized administrators.
- Encrypt sensitive backups where appropriate.
- Keep recovery credentials and encryption keys in a secure location separate from this repository.
- Protect backup storage against accidental deletion and unauthorized modification.
- Do not upload VM disks, database dumps, credentials, or sensitive infrastructure exports to a public repository.
- Review backup retention and deletion procedures periodically.

## 10. Change History

| Date           | Change                                             | Result               |
| -------------- | -------------------------------------------------- | -------------------- |
| To be recorded | Initial backup and disaster recovery documentation | Pending verification |
