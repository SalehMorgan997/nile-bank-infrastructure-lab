# Hyper-V Network Design

## 1. Purpose

This document describes the virtual networking design for the Nile Bank Enterprise IT Infrastructure Lab running on a Windows 11 Hyper-V host.

The lab is intended for controlled testing of Windows Server infrastructure, Active Directory, DNS, DHCP, Linux services, and monitoring.

## 2. Network Overview

| Setting | Design |
|---|---|
| Virtualization platform | Microsoft Hyper-V |
| Host operating system | Windows 11 |
| Virtual switch type | Internal |
| Planned lab subnet | `10.10.30.0/24` |
| Planned domain | `corp.nilebank.lab` |
| Network status | Verify against current configuration |

## 3. Internal Virtual Switch

A Hyper-V Internal virtual switch allows communication between virtual machines connected to that switch and the Windows host operating system.

An Internal switch does not automatically connect the lab to the physical network or provide internet access.

Internet connectivity requires a separately configured solution, such as host-based NAT or a routing VM. Any such configuration must be documented and tested independently.

## 4. Logical Network Layout

```text
Windows 11 Hyper-V Host
|
+-- Hyper-V Internal Virtual Switch
    |
    +-- DC01
    |   +-- Active Directory Domain Services
    |   +-- DNS (if installed and configured)
    |
    +-- DHCP Server (if deployed separately)
    |
    +-- Additional Windows Server VMs
    |   +-- File services
    |   +-- Print services
    |
    +-- Linux Server
    |
    +-- Zabbix Monitoring (if deployed)
    |
    +-- Client VMs (if deployed)
```

This is a logical design diagram. It does not confirm that every component is currently deployed or connected.

## 5. Network Configuration Requirements

- Connect each intended lab VM to the correct Hyper-V virtual switch.
- Use static IP addresses for infrastructure servers where appropriate.
- Ensure DHCP address pools do not overlap with statically assigned addresses.
- Configure domain-joined Windows clients to use the lab's internal DNS service.
- Configure a default gateway only when a valid routing path is available.
- Keep lab network changes separate from the host's normal network configuration.
- Record any NAT, routing, or internet-sharing configuration separately.

## 6. Validation Checklist

Mark an item complete only after testing it and recording the actual result.

- [ ] Confirm the Internal virtual switch exists in Hyper-V Manager.
- [ ] Confirm each VM is connected to the intended virtual switch.
- [ ] Verify IP addresses and subnet masks.
- [ ] Test communication between relevant VMs.
- [ ] Verify DNS resolution for the lab domain.
- [ ] Verify DHCP address allocation, if DHCP is configured.
- [ ] Verify internet connectivity separately, if required.
- [ ] Record any failures and the troubleshooting steps taken.

## 7. Troubleshooting Commands

On the Hyper-V host:

```powershell
Get-VMSwitch |
    Select-Object Name, SwitchType, NetAdapterInterfaceDescription
```

Inspect VM network adapters:

```powershell
Get-VMNetworkAdapter -All |
    Select-Object VMName, SwitchName, Status, IPAddresses
```

Inside a Windows VM:

```powershell
ipconfig /all
```

Inside a Linux VM:

```bash
ip addr
ip route
```

Use the command output to establish the actual configuration rather than relying solely on the planned design.

## 8. Security and Change Management

- Avoid exposing lab services directly to the internet.
- Do not change production or host network settings unnecessarily.
- Back up relevant configuration before significant network changes.
- Record the date, reason, expected impact, test results, and rollback steps for material changes.
- Never commit passwords, private keys, or other secrets to the repository.

## 9. Change History

| Date | Change | Result |
|---|---|---|
| To be recorded | Initial network design documentation | Pending verification |
