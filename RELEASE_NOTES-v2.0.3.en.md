# DComEasy v2.0.3

## Highlights

- **Clearer layout:** shorter English menu, template and action labels, improved narrow-window button layout, license-help scrolling and bottom spacing, and Chinese punctuation wrapping.
- **Actionable connection failures:** Connection shows the cause, where to act and the next steps. Original errors, network checks and execution context remain in history with preserved line breaks, without a duplicate bottom log panel.
- **Honest diagnostic scope:** local check results are separated from OPCEnum configuration reference. Sources and complete permission rules remain available; actual missing settings, empty ACLs and read failures are still reported. Exports use the same separation. Reading settings does not prove remote connectivity.
- **Updated guidance:** new 18-second Chinese and English walkthroughs show the current diagnostics, licensing, configuration, connection, monitoring and trend screens.

## Walkthroughs

[English MP4](https://github.com/Todayos/DComEasy-Releases/releases/download/v2.0.3/quick-start-v2.0.3-en-US.mp4) · [中文 MP4](https://github.com/Todayos/DComEasy-Releases/releases/download/v2.0.3/quick-start-v2.0.3-zh-CN.mp4)

All scenes use sample data, not real accounts, activation codes or servers. They are not evidence of a real site connection test. GIF previews are available on the repository home page.

## Upgrade

Close DComEasy and run `DComEasy-Setup-v2.0.3.exe` as administrator. Keep the existing installation directory for an in-place upgrade. License state, logs and connection history are preserved. The installer includes the required .NET runtime.

For a failed connection, review next steps on Connection and full details in History. Passing local checks does not replace a remote test from the actual client.

## Installer checksum

```text
SHA-256  be5fd10e5799969e19cc9d39bf9cf08095263cef4ac5b55c256334f384f4b6cb
```

The attached `SHA256SUMS.txt` also covers the installer and walkthroughs. Download only from this repository's official Releases.
