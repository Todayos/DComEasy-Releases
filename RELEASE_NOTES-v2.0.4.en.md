# DComEasy v2.0.4

## Highlights

- **Accurate DCOM configuration:** fixes default protocol reading and writing so diagnostics and the applied configuration agree.
- **Safer recovery after configuration failures:** refreshes the snapshot immediately before applying changes. Rollback preserves external changes made after previewing the plan and before execution starts.
- **Reliable component cancellation:** when DLL registration or repair is canceled, waits for related processes to finish and completes the required recovery before subsequent operations.
- **More complete monitoring recovery:** skips and reports damaged indexes without blocking other records, and recovers existing capture snapshots that were not yet indexed. Interrupted report generation can be retried to reduce missing records.
- **Consistent shutdown:** does not ask again after exit is confirmed. Repeated close requests during cleanup no longer leave an interactive window with stopped monitoring services.
- **Stable handling of extreme values:** improves range calculations for trends and PDF reports, preventing invalid ranges from breaking display or export when values are very large or very small.
- **More accurate capture completion:** a valid, complete final batch that crosses the end time can satisfy natural completion despite minor sampling jitter. Missing samples and collection failures still retain their warnings.

- **Updated guidance:** refreshed Chinese and English walkthroughs show the 2.0.4 diagnostics, licensing, configuration, connection, monitoring and trend screens.

## Upgrade

Close DComEasy and run `DComEasy-Setup-v2.0.4.exe` as administrator. Keep the existing installation directory for an in-place upgrade. License state, logs and connection history are preserved. The installer includes the required .NET runtime.

Interrupted monitoring report generation can be retried. Review recovered captures together with any missing-sample or failure warnings. Passing local checks does not replace a remote test from the actual client.

## Installer checksum

`DComEasy-Setup-v2.0.4.exe`

```text
6fa756a130fcf788c855ec1966570cb51cdf77470300cee0520da171a7b4b66c
```

The release includes `SHA256SUMS.txt` for the installer and both language versions of the videos and GIFs.
