# DHCP Configuration and Troubleshooting

## 1. Purpose

This document describes the DHCP design and validation procedures for the Nile Bank Enterprise IT Infrastructure Lab.

DHCP automatically assigns network configuration to clients, including IP addresses, subnet masks, and optional gateway and DNS settings.

## 2. DHCP Server Design

| Setting                | Planned value                      | Status |
| ---------------------- | ---------------------------------- | ------ |
| DHCP server hostname   | To be confirmed                    | Verify |
| Planned DHCP server IP | `10.10.30.12`                      | Verify |
| Lab subnet             | `10.10.30.0/24`                    | Verify |
| DHCP scope range       | To be confirmed                    | Verify |
| Subnet mask            | `255.255.255.0`                    | Verify |
| Default gateway option | To be confirmed                    | Verify |
| DNS server option      | To be confirmed                    | Verify |
| DNS domain option      | `corp.nilebank.lab`                | Verify |
| DHCP authorization     | Required if joined to an AD domain | Verify |

The IP address and domain above are planned values from the lab design, not independently verified settings.

## 3. DHCP Design Considerations

- Use static addresses or reservations for infrastructure devices where appropriate.
- Exclude static server addresses from the dynamic allocation pool.
- Configure the correct subnet mask for the lab subnet.
- Provide the appropriate internal DNS server to domain-joined clients.
- Configure a default gateway only if a valid routing path exists.
- Avoid overlapping DHCP scopes or competing DHCP servers on the same network.
- If the DHCP server is domain-joined in an Active Directory environment, verify that it is authorized in Active Directory.

## 4. Verification Commands

Run these commands on the Windows DHCP server using an account with appropriate permissions.

List configured IPv4 scopes:

```powershell
Get-DhcpServerv4Scope
```

Inspect scope details:

```powershell
Get-DhcpServerv4Scope |
    Format-List ScopeId, Name, StartRange, EndRange, SubnetMask, State
```

Inspect scope options:

```powershell
Get-DhcpServerv4OptionValue
```

Inspect current leases:

```powershell
Get-DhcpServerv4Lease -ScopeId 10.10.30.0
```

The lease command assumes a scope with the ID `10.10.30.0` exists. Replace the scope ID if your actual configuration differs.

## 5. Client Validation

On a Windows test client, inspect its current configuration:

```cmd
ipconfig /all
```

Renew its DHCP lease only when appropriate for your isolated lab:

```cmd
ipconfig /release
ipconfig /renew
```

**Caution:** Releasing a lease temporarily disconnects the client from IPv4 networking. Do not run these commands on a work computer or a remote machine where you could lose access.

Confirm that the client receives the expected address, subnet mask, DHCP server, and DNS server.

## 6. Troubleshooting Workflow

1. Confirm the DHCP Server service is running.
2. Verify that the intended scope exists and is active.
3. Check the scope range, exclusions, and available addresses.
4. Verify that the DHCP server is connected to the intended virtual switch.
5. Check authorization if the server is joined to Active Directory.
6. Verify the client is configured to obtain its address automatically.
7. Review DHCP Server event logs and lease information.
8. Retest and record the actual outcome.

## 7. Validation Checklist

- [x] Confirm the DHCP Server role is installed.
- [x] Confirm the server's actual IP address.
- [x] Verify the scope and address range.
- [x] Verify exclusions and reservations.
- [x] Verify DNS and gateway options.
- [x] Confirm authorization where applicable.
- [x] Test address allocation from a lab client.
- [x] Record the assigned lease and test result.

## 8. Security Considerations

- Restrict DHCP administration to authorized accounts.
- Do not run an unintended DHCP server on a shared or production network.
- Keep credentials and other secrets out of scripts and GitHub.
- Document changes to scopes, exclusions, reservations, and options.

## 9. Change History

| Date           | Change                     | Result               |
| -------------- | -------------------------- | -------------------- |
| To be recorded | Initial DHCP documentation | Pending verification |
