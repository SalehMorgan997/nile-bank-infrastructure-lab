# Linux Server Configuration and Troubleshooting

## 1. Purpose

This document records the Linux server's role in the Nile Bank Enterprise IT Infrastructure Lab, including network configuration, remote administration, service management, and troubleshooting.

The Linux server may also support infrastructure monitoring. Zabbix configuration and monitoring results will be documented separately.

## 2. Linux Server Design

| Setting               | Configuration                                 | Status |
| --------------------- | --------------------------------------------- | ------ |
| VM name               | To be confirmed                               | Verify |
| Linux distribution    | To be confirmed                               | Verify |
| Hostname              | To be confirmed                               | Verify |
| IP address            | To be confirmed                               | Verify |
| Virtual switch        | Internal, according to the current lab design | Verify |
| Primary purpose       | Linux administration and monitoring support   | Verify |
| Remote administration | SSH, if installed and enabled                 | Verify |

Record the actual settings from the running VM. Do not treat planned values as verified configuration.

## 3. Network Verification

Display the hostname:

```bash
hostnamectl
```

Display network interfaces and IP addresses:

```bash
ip address
```

Display the routing table:

```bash
ip route
```

Inspect DNS resolver configuration:

```bash
resolvectl status
```

If `resolvectl` is unavailable on the installed distribution, use the distribution's supported DNS inspection method.

Verify that the Linux server has the expected address and can reach the intended lab systems. An Internal Hyper-V switch does not automatically provide internet access; internet connectivity depends on the host and routing configuration.

## 4. Service Management

Check whether SSH is running:

```bash
sudo systemctl status ssh
```

On distributions where the service is named `sshd`, use:

```bash
sudo systemctl status sshd
```

List running services:

```bash
systemctl --type=service --state=running
```

Check listening TCP and UDP sockets:

```bash
sudo ss -tulpn
```

Only enable services that are required for the lab.

## 5. SSH Administration

If SSH is installed and enabled, test connectivity from an authorized client:

```bash
ssh username@LINUX_SERVER_IP
```

Replace `username` and `LINUX_SERVER_IP` with the actual account and server address.

Security practices:

- Prefer SSH keys where appropriate.
- Protect private keys and never commit them to GitHub.
- Use strong authentication and restrict access to authorized accounts.
- Do not expose SSH directly to the public internet without a carefully designed security configuration.

## 6. Storage and Resource Checks

Check filesystem usage:

```bash
df -h
```

Check memory usage:

```bash
free -h
```

Check processor and system load:

```bash
uptime
```

These commands help identify resource constraints that could affect Linux services or monitoring.

## 7. Troubleshooting Workflow

1. Confirm the VM is running in Hyper-V.
2. Check the hostname, network interfaces, IP address, and routing table.
3. Verify the target service is installed and running.
4. Check firewall rules and the relevant listening port.
5. Test connectivity from the intended client.
6. Inspect service logs with `journalctl` where supported.
7. Record the error, troubleshooting steps, and actual outcome.

## 8. Validation Checklist

- [x] Confirm the Linux distribution and version.
- [x] Record the hostname and actual IP address.
- [x] Verify the virtual switch and network configuration.
- [x] Confirm required services are running.
- [x] Test SSH from an authorized client, if enabled.
- [x] Check disk, memory, and system load.
- [x] Record actual test results and unresolved issues.

## 9. Security Considerations

- Keep the operating system and installed packages updated.
- Use least-privilege accounts and `sudo` appropriately.
- Avoid storing passwords, tokens, SSH private keys, or other secrets in the repository.
- Restrict network services to the clients that need them.
- Take backups before significant changes and document recovery procedures.

## 10. Change History

| Date           | Change                             | Result               |
| -------------- | ---------------------------------- | -------------------- |
| To be recorded | Initial Linux server documentation | Pending verification |
