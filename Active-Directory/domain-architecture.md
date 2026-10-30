# Active Directory Domain Architecture

## 1. Purpose

This document describes the Active Directory design for the Nile Bank Enterprise IT Infrastructure Lab. It records the domain structure, domain controller roles, DNS dependencies, and client authentication tests.

The document distinguishes planned architecture from verified implementation.

## 2. Domain Design

| Setting                      | Value                   | Status |
| ---------------------------- | ----------------------- | ------ |
| DNS domain name              | `corp.nilebank.lab`     | Verify |
| NetBIOS domain name          | `NILEBANK`              | Verify |
| Primary domain controller    | `DC01`                  | Verify |
| Additional domain controller | `DC02`, if deployed     | Verify |
| DNS integration              | To be confirmed         | Verify |
| Domain-joined client         | `Client01`, if deployed | Verify |

## 3. Logical Architecture

```text
Nile Bank Lab Domain
corp.nilebank.lab
|
+-- DC01
|   +-- Active Directory Domain Services
|   +-- DNS, if installed and configured
|
+-- DC02 (optional)
|   +-- Additional domain controller
|   +-- Replication and redundancy testing
|
+-- Domain-Joined Clients
    +-- Authentication
    +-- Group Policy processing
    +-- Access to authorized resources
```

This diagram represents the intended logical structure, not proof that all components have been deployed.

## 4. Core Dependencies

- Active Directory Domain Services provides domain authentication and directory services.
- DNS enables domain clients to locate domain controllers and other domain services.
- Domain-joined clients must use appropriate internal DNS servers.
- Group Policy applies configuration according to scope, security filtering, and other policy settings.
- An additional domain controller requires appropriate DNS, network connectivity, and healthy directory replication.

## 5. Verification Commands

Run the relevant commands on the appropriate domain controller or domain-joined Windows machine.

Check domain membership:

```powershell
Get-CimInstance Win32_ComputerSystem |
    Select-Object Name, Domain, PartOfDomain
```

Inspect domain controller discovery:

```cmd
nltest /dsgetdc:corp.nilebank.lab
```

Inspect DNS configuration:

```cmd
ipconfig /all
```

Check domain controller and replication information when multiple domain controllers are deployed:

```cmd
repadmin /replsummary
```

The replication command is relevant only when the lab has multiple domain controllers configured.

## 6. Validation Checklist

- [x] Confirm the actual Active Directory domain name.
- [x] Confirm DC01 is configured as a domain controller.
- [x] Verify DNS records and domain controller discovery.
- [x] Confirm a test client can join the domain, if applicable.
- [x] Verify successful domain authentication.
- [x] Verify Group Policy processing on a test client.
- [x] If DC02 exists, test directory replication and document actual results.

Record the date, commands, results, and any errors for each completed test.

## 7. Security Considerations

- Use separate administrative accounts where appropriate.
- Apply least-privilege permissions.
- Keep Domain Administrator credentials out of scripts and documentation.
- Never publish passwords, DSRM secrets, private keys, or sensitive screenshots.
- Perform disruptive domain controller tests only in the isolated lab, with a recovery plan.

## 8. Change History

| Date           | Change                                              | Result               |
| -------------- | --------------------------------------------------- | -------------------- |
| To be recorded | Initial Active Directory architecture documentation | Pending verification |
