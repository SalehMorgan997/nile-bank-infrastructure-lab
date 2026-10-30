# File Server and SMB Permissions

## 1. Purpose

This document describes the design and validation procedures for file sharing in the Nile Bank Enterprise IT Infrastructure Lab.

The objective is to provide controlled access to shared folders using SMB, Windows share permissions, NTFS permissions, and Active Directory security groups where configured.

## 2. File Server Design

| Setting              | Planned configuration                | Status |
| -------------------- | ------------------------------------ | ------ |
| File server hostname | To be confirmed                      | Verify |
| Server IP address    | To be confirmed                      | Verify |
| Operating system     | Windows Server                       | Verify |
| SMB file sharing     | SMB 2/3, as supported and configured | Verify |
| Domain membership    | `corp.nilebank.lab`                  | Verify |
| Shared folders       | To be documented                     | Verify |
| Access control       | Share and NTFS permissions           | Verify |

## 3. Permission Design Principles

- Grant permissions to security groups rather than individual users wherever practical.
- Apply least privilege: users should receive only the access required for their tasks.
- Review both share permissions and NTFS permissions when troubleshooting access.
- Avoid granting Everyone or broad user groups Full Control without a documented reason.
- Keep administrative access separate from ordinary user access.
- Document the purpose, owner, and intended access group for each share.

## 4. Share and NTFS Permissions

SMB share permissions control access through the network share. NTFS permissions control access to files and folders on an NTFS volume.

When accessing a folder through SMB, effective access depends on both sets of permissions. A restrictive permission in either layer can limit the resulting access.

Example design — replace these names with the actual groups and paths used in the lab:

| Share          | Intended access                  | Example group          |
| -------------- | -------------------------------- | ---------------------- |
| DepartmentData | Read and modify                  | `GG_Department_Modify` |
| PublicRead     | Read only                        | `GG_Public_Read`       |
| ITAdmin        | Restricted administrative access | `GG_IT_Admins`         |

These are illustrative examples, not confirmed shares or groups in the current lab.

## 5. Verification Commands

Run the following on the file server using an account with appropriate permissions.

List SMB shares:

```powershell
Get-SmbShare
```

Inspect share permissions:

```powershell
Get-SmbShareAccess -Name "DepartmentData"
```

Replace `DepartmentData` with the actual share name.

Inspect NTFS access control entries:

```powershell
Get-Acl "D:\Shares\DepartmentData" |
    Format-List
```

Replace the example path with the actual folder path.

Inspect SMB server configuration:

```powershell
Get-SmbServerConfiguration |
    Select-Object EnableSMB1Protocol,
                  EnableSMB2Protocol,
                  EnableSecuritySignature,
                  RequireSecuritySignature,
                  EnableEncryptData
```

Interpret these settings in context. Do not disable SMB security features simply to make a connection work. SMB 1.0 should remain disabled unless a specifically justified legacy requirement exists.

## 6. Client Access Testing

From an authorized Windows client, test the share using its actual server name and share name:

```powershell
Test-NetConnection FILESERVER -Port 445
```

Replace `FILESERVER` with the real hostname.

Open the share in File Explorer using:

```text
\\FILESERVER\DepartmentData
```

Verify both successful access for authorized users and denied access for users who should not have permission.

Record the test account's security group membership, the share permissions, the NTFS permissions, and the observed result. Do not include passwords or sensitive user information.

## 7. Troubleshooting Workflow

1. Confirm the file server is reachable and resolves to the expected IP address.
2. Test TCP port 445 from the client.
3. Confirm the SMB share exists and is available.
4. Review share permissions and NTFS permissions.
5. Verify the user's current group membership and sign-in token.
6. Check Windows Firewall and relevant SMB settings.
7. Review applicable event logs.
8. Retest with an authorized account and record the result.

## 8. Validation Checklist

- [x] Confirm the file server hostname and IP address.
- [x] Verify SMB shares exist.
- [x] Document share permissions.
- [x] Document NTFS permissions.
- [x] Test access using an authorized account.
- [x] Test that unauthorized access is denied.
- [x] Verify SMB 1.0 is disabled unless a justified exception exists.
- [x] Record troubleshooting results and any configuration changes.

## 9. Security Considerations

- Do not expose SMB directly to the public internet.
- Use least-privilege permissions and review group membership regularly.
- Keep sensitive documents and credentials out of GitHub.
- Do not weaken SMB security settings as a first-line troubleshooting measure.
- Document permission changes and their justification.

## 10. Change History

| Date           | Change                            | Result               |
| -------------- | --------------------------------- | -------------------- |
| To be recorded | Initial file server documentation | Pending verification |
