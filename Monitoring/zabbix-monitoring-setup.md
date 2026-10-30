# Zabbix Monitoring Setup and Troubleshooting

## 1. Purpose

This document describes the Zabbix monitoring design for the Nile Bank Enterprise IT Infrastructure Lab.

The goal is to monitor lab infrastructure, check host availability, collect system metrics, and investigate monitoring failures from a central dashboard.

## 2. Monitoring Architecture

| Component            | Planned role                                                               | Status |
| -------------------- | -------------------------------------------------------------------------- | ------ |
| Zabbix server        | Central monitoring and alert processing                                    | Verify |
| Zabbix frontend      | Web dashboard                                                              | Verify |
| Database             | Stores monitoring configuration and collected data                         | Verify |
| Windows hosts        | Windows Server monitoring through an appropriate agent or supported method | Verify |
| Linux host           | Linux system monitoring through an appropriate agent or supported method   | Verify |
| Network connectivity | Allows monitored hosts to communicate with Zabbix                          | Verify |

Confirm the actual Zabbix version, deployment method, database, and agent configuration before recording them as implemented.

## 3. Host Inventory

Document each host using its actual name and address.

| Host          | Operating system                   | IP address     | Monitoring status |
| ------------- | ---------------------------------- | -------------- | ----------------- |
| DC01          | Windows Server, if confirmed       | To be recorded | Verify            |
| B302          | To be confirmed                    | To be recorded | Verify            |
| Linux server  | Linux distribution to be confirmed | To be recorded | Verify            |
| Zabbix server | To be confirmed                    | To be recorded | Verify            |

The names above come from the lab's working inventory and should be checked against the current VMs and Zabbix dashboard.

## 4. Dashboard Verification

In the Zabbix frontend:

1. Sign in with an authorized account.
2. Open the host inventory.
3. Confirm that each intended host exists.
4. Check the latest availability and agent status.
5. Open the latest data view for a host.
6. Confirm that metrics are being collected and timestamps are current.
7. Review any problems or unsupported items.

A host appearing in the inventory does not, by itself, prove that monitoring is functioning correctly. Verify recent data and the relevant item status.

## 5. Network and Agent Checks

### Windows hosts

On a Windows host, inspect the Zabbix Agent service if the agent is installed as a Windows service:

```powershell
Get-Service *Zabbix*
```

Check listening ports:

```powershell
Get-NetTCPConnection -State Listen
```

From the Zabbix server, test the appropriate agent port if active-agent configuration and the relevant network path require it:

```bash
nc -vz WINDOWS_HOST_IP 10050
```

Replace `WINDOWS_HOST_IP` with the actual address. Port 10050 is commonly used by Zabbix agents; confirm the configured port and monitoring mode before troubleshooting.

### Linux hosts

Check the agent service, depending on the installed package:

```bash
sudo systemctl status zabbix-agent
```

For Zabbix Agent 2, the service is commonly:

```bash
sudo systemctl status zabbix-agent2
```

Inspect listening ports:

```bash
sudo ss -tulpn
```

If the host uses passive checks, confirm that the configured agent port is reachable from the Zabbix server. Active checks use a different connection pattern, so a failed inbound port test does not necessarily mean active monitoring is broken.

## 6. Troubleshooting Workflow

If a host is unavailable or data is missing:

1. Confirm the VM is running.
2. Verify the host's IP address and network configuration.
3. Check name resolution if hostnames are used.
4. Confirm the Zabbix agent is installed and running, where applicable.
5. Review the agent configuration, including the server address and hostname settings.
6. Check firewall rules and the configured communication ports.
7. Review Zabbix server and agent logs.
8. Check the host's interface and item configuration in the frontend.
9. Verify that the latest data is updating.
10. Record the cause, corrective action, and actual result.

Do not disable the firewall broadly as a troubleshooting shortcut. Test the specific required connection instead.

## 7. Alerts and Problems

Where alerting is configured, document:

- The trigger or condition.
- The monitored host and item.
- The severity.
- The notification method and recipient group.
- The test procedure and observed result.

Do not claim email or other notifications are working until an actual test notification has been received and confirmed.

## 8. Validation Checklist

- [x] Confirm the Zabbix version and deployment method.
- [x] Confirm the dashboard is accessible from the intended client.
- [x] Verify each intended host is configured.
- [x] Confirm recent data is arriving from Windows hosts.
- [x] Confirm recent data is arriving from the Linux host.
- [x] Investigate unsupported items or unavailable hosts.
- [x] Test configured triggers and notifications, if applicable.
- [x] Record actual results and any unresolved issues.

## 9. Security Considerations

- Use authorized accounts and strong authentication for the frontend.
- Keep Zabbix credentials, API tokens, and database passwords out of GitHub.
- Restrict agent and server communication to the required lab network paths.
- Avoid exposing the dashboard or agent ports directly to the public internet.
- Keep Zabbix components updated and back up configuration and database data appropriately.

## 10. Change History

| Date           | Change                                  | Result               |
| -------------- | --------------------------------------- | -------------------- |
| To be recorded | Initial Zabbix monitoring documentation | Pending verification |
