# Print Server Configuration and Troubleshooting

## 1. Purpose

This document describes the design, administration, and troubleshooting procedures for centralized printing in the Nile Bank Enterprise IT Infrastructure Lab.

The objective is to document shared printers, print queues, driver management, permissions, and client connectivity.

## 2. Print Server Design

| Setting                          | Planned configuration             | Status |
| -------------------------------- | --------------------------------- | ------ |
| Print server hostname            | To be confirmed                   | Verify |
| Server IP address                | To be confirmed                   | Verify |
| Operating system                 | Windows Server                    | Verify |
| Print and Document Services role | To be confirmed                   | Verify |
| Shared printers                  | To be documented                  | Verify |
| Print queue permissions          | Least-privilege access            | Verify |
| Client connections               | Windows test clients, if deployed | Verify |

## 3. Core Components

- **Print server:** Hosts and manages shared printer queues.
- **Print queue:** Stores and manages print jobs waiting for processing.
- **Printer driver:** Enables the operating system to communicate with the printer.
- **Client connection:** Allows authorized users to submit jobs to a shared printer.
- **Permissions:** Control who can print and who can administer the printer.

This design does not assume a physical printer is connected. A lab can document the role and test queues without claiming that physical printing has been tested.

## 4. Verification Commands

Run these commands on the Windows print server with appropriate permissions.

List installed printers:

```powershell
Get-Printer
```

Inspect print jobs:

```powershell
Get-PrintJob -PrinterName "PrinterName"
```

Replace `PrinterName` with an actual queue name.

Inspect the Print Spooler service:

```powershell
Get-Service Spooler
```

Check the Print and Document Services role, where applicable:

```powershell
Get-WindowsFeature Print-Server
```

The last command is intended for Windows Server systems that provide the Server Manager PowerShell module.

## 5. Client Connectivity Testing

From an authorized Windows client, verify that the print server resolves to the expected address:

```powershell
Test-NetConnection PRINTSERVER -Port 445
```

Replace `PRINTSERVER` with the actual server hostname.

For a shared printer, the connection path commonly follows this format:

```text
\\PRINTSERVER\PrinterShare
```

Replace the example names with the actual print server and shared printer name.

A successful TCP 445 test confirms SMB connectivity to that endpoint; it does not prove that the printer queue, driver, or physical printer is working.

## 6. Troubleshooting Workflow

1. Confirm the print server is reachable and its hostname resolves correctly.
2. Check that the Print Spooler service is running.
3. Verify that the printer queue exists and is shared if network access is intended.
4. Check the queue's permissions and the user's authorization.
5. Review driver compatibility and installation errors.
6. Inspect the queue for stuck or failed jobs.
7. Review relevant PrintService event logs.
8. Restart the Print Spooler only when appropriate, because doing so can interrupt printing and affect queued jobs.
9. Retest and record the actual result.

Avoid deleting queued jobs or restarting services before checking the impact.

## 7. Validation Checklist

- [x] Confirm the print server hostname and IP address.
- [x] Verify the Print Server role, if installed.
- [x] Confirm the Print Spooler service status.
- [x] Document available printer queues and share names.
- [x] Verify permissions for authorized users.
- [x] Test client connectivity.
- [x] Test a print job if a suitable printer or test queue is available.
- [x] Record any errors, fixes, and final results.

## 8. Security Considerations

- Restrict printer administration to authorized accounts.
- Install drivers from trusted sources.
- Avoid granting broad administrative permissions unnecessarily.
- Do not expose print services directly to the public internet.
- Document service restarts, driver changes, and queue modifications.

## 9. Change History

| Date           | Change                             | Result               |
| -------------- | ---------------------------------- | -------------------- |
| To be recorded | Initial print server documentation | Pending verification |
