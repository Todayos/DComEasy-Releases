# DComEasy

![DComEasy — Windows OPC DA / DCOM configuration and diagnostics](assets/banner-en.svg)

<p align="center">
  <a href="README.md">简体中文</a> · <strong>English</strong>
</p>

<p align="center">
  <a href="https://github.com/Todayos/DComEasy-Releases/releases/latest"><strong>Download the latest release</strong></a>
  · <a href="docs/usage.en.md">User guide</a>
  · <a href="https://github.com/Todayos/DComEasy-Releases/issues">Issue tracker</a>
</p>

DComEasy is a Windows OPC DA / DCOM configuration and diagnostic tool for industrial deployment, commissioning, and maintenance. It brings environment diagnostics, DCOM permission configuration, OPC DA connection testing, point monitoring, network checks, and diagnostic reports into one interface.

> [!IMPORTANT]
> DComEasy is proprietary software. This repository hosts official releases, user documentation, and issue tracking. It does not contain the product source code. By downloading or using the software, you agree to the license terms included with the release package.

## Features

- **Configuration diagnostics**: inspect DCOM, OPC Core Components, OPCEnum, permissions, and protocol status with actionable guidance.
- **Configuration management**: validate or create a local OPC user, preview changes, and apply DCOM permissions, authentication levels, and protocol settings.
- **OPC DA connection testing**: connect by ProgID or CLSID and inspect network checks, failure stages, error codes, and original errors.
- **Node browsing and monitoring**: browse OPC nodes, query full ItemIDs, read points, and set individual or batch polling intervals.
- **Network diagnostics**: check target connectivity, ports, local listeners, and firewall status, then add local inbound rules when needed.
- **Diagnostic reports**: export selectable and copyable PDF or standalone HTML reports for troubleshooting, handover, and archiving.
- **Bilingual interface**: switch between Simplified Chinese and English while retaining the selected language.

## Screenshots

### Connected server and node browser

![DComEasy OPC DA connection and node browser](assets/screenshots/connection-zh-CN.png)

### One-time read

Read a selected point once to display its current value, quality, and server timestamp without enabling scheduled polling.

![DComEasy OPC DA one-time read](assets/screenshots/single-read-zh-CN.png)

### Batch scheduled polling

Select multiple points and apply one polling interval to all of them. Both points below use a five-second interval.

![DComEasy OPC DA batch scheduled polling](assets/screenshots/batch-refresh-5s-zh-CN.png)

## Editions

| Feature | Free | Professional |
| --- | :---: | :---: |
| Configuration diagnostics, user validation, and change preview | ✓ | ✓ |
| OPC DA connection testing, node browsing, and one-time reads | ✓ | ✓ |
| Network, port, and firewall status checks | ✓ | ✓ |
| PDF diagnostic reports | Watermarked | No watermark |
| Create local OPC users and apply DCOM configuration | — | ✓ |
| Install and repair the OPC runtime environment | — | ✓ |
| Continuous polling and batch monitoring | — | ✓ |
| Add firewall rules automatically | — | ✓ |
| HTML diagnostic reports | — | ✓ |

## Requirements

- Supports 64-bit Windows. DComEasy runs as a 32-bit process for compatibility with OPC DA and related COM components.
- Administrator privileges to install and run DComEasy.
- The complete offline installer, which includes the required .NET runtime.
- A reachable OPC DA server and valid OPC user credentials for connection testing.

## Download and installation

1. Download the latest `DComEasy-Setup-v1.0.0.exe` from [Releases](https://github.com/Todayos/DComEasy-Releases/releases).
2. Run the installer as an administrator.
3. Start DComEasy from the Start menu and run it with administrator privileges when prompted.

Use installers published through this repository's GitHub Releases. Do not download installers from unknown sources or copy only the application executable from an installation directory.

See the [user guide](docs/usage.en.md) for detailed instructions.

## Feedback

Search the [existing issues](https://github.com/Todayos/DComEasy-Releases/issues) before opening a new one. If no matching issue exists, use one of the templates:

- [Report a bug](https://github.com/Todayos/DComEasy-Releases/issues/new?template=bug_report.yml)
- [Request a feature](https://github.com/Todayos/DComEasy-Releases/issues/new?template=feature_request.yml)

Include the DComEasy version, Windows version, reproduction steps, expected result, and actual result. Remove account names, host names, IP addresses, and other sensitive information from screenshots and logs. Never submit passwords or activation codes.

## Copyright and license

Copyright © 2026 Todayos. All rights reserved.

DComEasy is proprietary software. Public access to this repository does not grant permission to copy, modify, redistribute, reverse engineer, or use the software commercially. The license terms included with each release package govern use of the software. Third-party components remain subject to their respective licenses.
