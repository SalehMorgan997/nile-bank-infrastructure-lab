# IP Addressing Plan

## 1. Overview

This document records the IP addressing design for the Nile Bank Hyper-V lab.

**Planned subnet:** `10.10.30.0/24`
**Subnet mask:** `255.255.255.0`
**Virtual switch:** Hyper-V Internal

The values below must be verified against the current VM network configuration before being treated as confirmed implementation details.

## 2. Server Addressing

| Hostname / Role                     | Planned IP address         | Assignment               | Status |
| ----------------------------------- | -------------------------- | ------------------------ | ------ |
| DC01 — Domain Controller            | `10.10.30.10`              | Static                   | Verify |
| DHCP Server                         | `10.10.30.12`              | Static                   | Verify |
| DC02 — Additional Domain Controller | To be confirmed            | Static, if deployed      | Verify |
| File Server                         | To be confirmed            | Static, if deployed      | Verify |
| Print Server                        | To be confirmed            | Static, if deployed      | Verify |
| Linux Server                        | To be confirmed            | Depends on configuration | Verify |
| Zabbix Server                       | To be confirmed            | Depends on configuration | Verify |
| Client VMs                          | DHCP scope to be confirmed | DHCP, if configured      | Verify |

## 3. Network Configuration

| Setting              | Value           |
| -------------------- | --------------- |
| Network address      | `10.10.30.0`    |
| Prefix length        | `/24`           |
| Subnet mask          | `255.255.255.0` |
| Default gateway      | To be confirmed |
| DNS server addresses | To be confirmed |
| DHCP scope range     | To be confirmed |

An Internal Hyper-V switch does not automatically provide internet access. A gateway or routing solution must be configured separately if internet connectivity is required.

## 4. Address Allocation Rules

- Reserve static addresses for infrastructure servers.
- Ensure DHCP does not allocate addresses already assigned statically.
- Configure domain-joined clients to use the appropriate internal DNS server.
- Document the actual DHCP scope, exclusions, reservations, and lease duration once verified.
- Record any gateway, routing, or NAT configuration separately.

## 5. Validation Checklist

Record the actual results when testing:

- [x] Confirm each VM's IP address using `ipconfig /all` on Windows or `ip addr` on Linux.
- [x] Confirm subnet masks and default gateways.
- [x] Verify DNS resolution for the lab domain.
- [x] Verify DHCP clients receive the intended addresses.
- [x] Test connectivity between the relevant VMs.
- [x] Confirm the DHCP scope does not conflict with static assignments.

## 6. Change History

Update this section when the addressing plan changes.

| Date           | Change                           | Result               |
| -------------- | -------------------------------- | -------------------- |
| To be recorded | Initial addressing documentation | Pending verification |

