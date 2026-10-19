# DComEasy v2.0.2

## Changes

- **Safer OPC accounts**: new local OPC accounts use passwords that never expire. The installer includes a script to inspect and repair accounts created by older DComEasy releases without deleting the account or changing its password.
- **Clearer credential actions**: credentials are validated automatically. Click the status icon to retry and copy the complete diagnostic from the status text. The **Manage user** menu always shows Create user, Delete local account, and Clear credentials. Create user is enabled only when the local account is confirmed missing; clearing credentials leaves the Windows account intact. Deletion checks the account name and SID first. Menu hover highlights the full row.
- **Readable Boolean values**: switches display as `0/1` in the monitoring list and trends and can be used by numeric threshold rules. Values actually returned as empty remain empty.

## Upgrade

Close DComEasy, then run `DComEasy-Setup-v2.0.2.exe` as an administrator. Keep the prefilled installation directory for an in-place upgrade. License state, logs, and connection history are preserved. The installer includes the required .NET runtime.

Existing OPC accounts are not deleted or given a new password. To inspect an account created by an older DComEasy release, open PowerShell as administrator in the installation directory and run:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\tools\Repair-DComEasyOpcUser.ps1 -UserName <account>
```

After reviewing the result, add `-Apply` to repair its expiry setting. Deleting and recreating an account gives it a new SID, so DCOM permissions may need to be configured again.

## Installer checksum

```text
SHA-256  4878c15752cac27f6594dcda3fb9f4b081547b617bb86afead84d6440ff5512a
```

Download the installer only from an official Release in this repository.
