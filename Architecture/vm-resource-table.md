# Virtual Machine Resource Table

## 1. Overview

This document records the hardware resources available to the Hyper-V host and the resources assigned to each virtual machine in the Nile Bank Enterprise IT Infrastructure Lab.

Resource allocations must be verified against the current Hyper-V configuration before being marked as confirmed.

## 2. Hyper-V Host

| Component | Specification | Status |
|---|---|---|
| Host operating system | Windows 11 | Confirmed by project notes |
| CPU | AMD Ryzen 5 2600X | Confirmed by project notes |
| Physical memory | 16 GB RAM | Confirmed by project notes |
| Hypervisor | Microsoft Hyper-V | Confirmed by project notes |
| Virtual switch | Internal | Verify current configuration |
| Storage capacity | To be recorded | Pending |
| Available memory during lab operation | To be measured | Pending |

## 3. Virtual Machine Inventory

| VM name | Role | Operating system | vCPU | RAM | Status |
|---|---|---|---:|---:|---|
| DC01 | Primary domain controller | Windows Server | Verify | Verify | Verify |
| DC02 | Additional domain controller, if deployed | Windows Server | Verify | Verify | Verify |
| DHCP01 | DHCP server, if deployed separately | Windows Server | Verify | Verify | Verify |
| File Server | File services, if deployed | Windows Server | Verify | Verify | Verify |
| Print Server | Print services, if deployed | Windows Server | Verify | Verify | Verify |
| Linux Server | Linux services | Linux distribution to confirm | Verify | Verify | Verify |
| Zabbix Server | Monitoring, if deployed separately | Linux distribution to confirm | Verify | Verify | Verify |
| Client01 | Domain-joined test client, if deployed | To be confirmed | Verify | Verify | Verify |

**Important:** This is an inventory template, not confirmation that every listed VM currently exists. Update it to match the actual lab.

## 4. Resource Allocation Guidelines

- Record the actual vCPU count and assigned memory for each VM.
- Distinguish startup memory from minimum and maximum memory if Hyper-V Dynamic Memory is enabled.
- Avoid allocating all host memory to virtual machines; Windows 11 and Hyper-V require memory to remain available.
- Monitor host and VM performance while multiple servers are running.
- Increase allocations only when testing shows a need and the host has sufficient resources.
- Record storage usage and virtual disk type where relevant.

## 5. Verification Commands

Run these PowerShell commands on the Hyper-V host to inspect the VM configuration.

List virtual machines:

```powershell
Get-VM | Select-Object Name, State, ProcessorCount, MemoryStartup
```

Inspect memory settings:

```powershell
Get-VM | Select-Object Name, DynamicMemoryEnabled,
    MemoryStartup, MemoryMinimum, MemoryMaximum
```

Inspect virtual network adapters and switches:

```powershell
Get-VMNetworkAdapter -All |
    Select-Object VMName, Name, SwitchName, IPAddresses
```

Use the output to replace `Verify` with actual values. If a command returns an error, check that PowerShell is running with the appropriate Hyper-V permissions.

## 6. Change History

| Date | Change | Result |
|---|---|---|
| To be recorded | Initial VM resource inventory | Pending verification |
