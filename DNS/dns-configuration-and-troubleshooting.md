# DNS Configuration and Troubleshooting

## 1. Purpose

This document records the DNS design, configuration checks, and troubleshooting procedures for the Nile Bank Enterprise IT Infrastructure Lab.

DNS is a critical dependency for Active Directory because domain clients use DNS to locate domain controllers and related services.

## 2. DNS Design

| Setting                   | Planned configuration                      | Status |
| ------------------------- | ------------------------------------------ | ------ |
| Lab domain                | `corp.nilebank.lab`                        | Verify |
| Primary domain controller | `DC01`                                     | Verify |
| DNS server                | To be confirmed                            | Verify |
| DNS zone                  | `corp.nilebank.lab`                        | Verify |
| Zone type                 | Active Directory-integrated, if configured | Verify |
| Client DNS configuration  | Internal DNS server                        | Verify |
| Forwarders                | To be confirmed                            | Verify |

Do not assume that DNS is installed on DC01 or that the zone is Active Directory-integrated until you have checked the actual configuration.

## 3. Core DNS Requirements

- Domain-joined clients must use DNS servers capable of resolving the lab's Active Directory records.
- The DNS zone must contain the records needed for domain controller discovery.
- DNS settings must be consistent with the lab's network design.
- External name resolution may require configured forwarders or another appropriate resolution method.
- If multiple DNS servers are deployed, test each one independently.

## 4. Verification Commands

### On a Windows DNS server

List DNS zones:

```powershell
Get-DnsServerZone
```

Inspect DNS records for the lab zone:

```powershell
Get-DnsServerResourceRecord -ZoneName "corp.nilebank.lab"
```

These commands require the relevant DNS Server PowerShell tools and permissions.

### On a Windows client or server

Check network and DNS settings:

```cmd
ipconfig /all
```

Test resolution of the lab domain:

```cmd
nslookup corp.nilebank.lab
```

Test domain controller discovery:

```cmd
nltest /dsgetdc:corp.nilebank.lab
```

Query Active Directory's domain controller locator records:

```cmd
nslookup -type=SRV _ldap._tcp.dc._msdcs.corp.nilebank.lab
```

Record the actual output, DNS server queried, and any errors.

## 5. Troubleshooting Workflow

1. Check the client's IP address, subnet mask, gateway, and DNS server addresses.
2. Confirm the configured DNS server is reachable from the client.
3. Query the DNS server directly using `nslookup`.
4. Check whether the required domain and SRV records exist.
5. Verify that the DNS service is running and the relevant zone is loaded.
6. Check domain controller discovery using `nltest`.
7. Review relevant DNS Server and System event logs.
8. Retest after each change and record the result.

Do not change DNS settings on multiple servers at once. Identify the cause first and document any configuration changes.

## 6. Validation Checklist

- [x] Confirm the DNS Server role is installed where expected.
- [x] Confirm the lab DNS zone exists.
- [x] Verify the domain controller's A record.
- [x] Verify the relevant Active Directory SRV records.
- [x] Confirm clients use the intended internal DNS server.
- [x] Test domain controller discovery from a client.
- [x] Test external name resolution only if internet connectivity is configured.
- [x] Record failures, fixes, and final test results.

## 7. Security Considerations

- Restrict DNS administration to authorized accounts.
- Avoid publishing internal screenshots that expose sensitive organizational details.
- Do not commit passwords, private keys, or other secrets.
- Document changes to DNS records and forwarders.

## 8. Change History

| Date           | Change                    | Result               |
| -------------- | ------------------------- | -------------------- |
| To be recorded | Initial DNS documentation | Pending verification |
