# DComEasy User Guide

[Home](../README.en.md) · [简体中文](usage.md) · [Latest release](https://github.com/Todayos/DComEasy-Releases/releases/latest)

## Install and start

1. Download the complete offline installer from [Releases](https://github.com/Todayos/DComEasy-Releases/releases).
2. Right-click the installer and select **Run as administrator**.
3. Start DComEasy from the Start menu after installation.
4. DComEasy requires administrator privileges to inspect and change system-level DCOM settings. A normal launch displays a reminder and exits.

The installer includes the required .NET runtime. Do not copy only `DComEasy.exe` from the installation directory because required components may be missing.

## Configuration diagnostics

Open **Diagnostics** and select **Run Check**. DComEasy inspects local OPC DA / DCOM settings, components, permissions, and protocols. Diagnosis does not change system settings or start services.

Each result includes its status and guidance. After diagnosis, export a PDF report when you need an archive; the Professional edition can also export standalone HTML.

## Apply configuration

Open **Configuration**, then:

1. Enter and validate the OPC user. The Professional edition can create a local user when required.
2. Select the authentication level, protocols, and DCOM permissions needed for the target environment.
3. Preview the proposed changes.
4. Apply the configuration after reviewing every change, then inspect each result.

DCOM settings affect system security and remote access. Review the environment's security requirements and grant only the permissions that are needed.

## Test an OPC DA connection

Connection testing does not require a prior diagnosis or configuration run:

1. Validate the OPC user on the Configuration page.
2. Open **Connection**, then enter the target host and probe port.
3. Enter the OPC server ProgID or CLSID. CLSID takes precedence when both are supplied.
4. Start the test and review network checks, server activation, and status results.

Successful and failed attempts are stored in connection history without passwords. Error details and table content can be copied for troubleshooting.

## Browse and monitor nodes

After connecting, expand the OPC node tree or query a full ItemID. Add points to the monitoring list and use the context menu to read once, configure a 1–3600 second polling interval, apply batch polling, stop monitoring, remove points, or copy values and errors.

Points and polling settings remain only in the current target session.

## Network diagnostics

Open **Network**, enter a host and port, and start the check. Remote checks cover host resolution, Ping, and the target TCP port. Local checks also show listeners and a summary of matching firewall rules.

The Professional edition can add local TCP or UDP inbound rules in batches. A firewall rule permits traffic but does not start the service that listens on the port.

## Licensing

The **License** page shows the edition, license status, machine identifier, and expiry. The Professional edition uses a 16-character offline activation code. Never include an activation code in a public issue, screenshot, or log.

## Troubleshooting

- A completed local configuration does not prove that a remote OPC DA connection will succeed. Use the connection test to identify the failing stage.
- Ping can fail while a TCP port remains reachable when ICMP is disabled. Review each check independently.
- Some OPC servers do not expose a complete hierarchy. Refresh the directory or query a full ItemID.

Before reporting a problem, search the [existing issues](https://github.com/Todayos/DComEasy-Releases/issues). Use the [bug report template](https://github.com/Todayos/DComEasy-Releases/issues/new?template=bug_report.yml) and include the DComEasy version, Windows version, reproduction steps, and complete error text. Remove passwords, activation codes, account names, host names, IP addresses, and other sensitive information first.
