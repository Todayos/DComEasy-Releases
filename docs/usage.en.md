# User guide

[Project home](../README.md) · [简体中文](usage.md) | English · [License](licensing/LICENSE.en.txt)

## Startup and language

Run the offline `DComEasy-Setup-v2.0.4.exe` as an administrator. On first installation, choose a directory (the default is `DComEasy` under 32-bit Program Files). Use a local directory that all relevant Windows accounts can read and execute; a private Downloads or Desktop directory may still cause cross-account connection probes to fail. The target directory must be empty. If an all-users Desktop or Start menu shortcut named DComEasy already exists, inspect and rename or move it first; setup will not overwrite it. To install a newer release, close DComEasy and run the newer installer as an administrator without uninstalling first. Setup still shows the directory page and defaults to the registered installation directory. Keep that directory for an in-place upgrade, or choose another empty directory for the new version. When another directory is selected, registration and managed shortcuts point to it; files in the previous directory are not deleted or moved. License state, ProgramData logs and backups, per-user connection history, and user-owned files are preserved. Launch DComEasy from the all-users Desktop or Start menu shortcut as an administrator. A normal launch only displays “Please open this application with administrator privileges.” and exits after acknowledgment; it does not elevate itself. The installer includes the .NET runtime and needs no network access on the target PC. It does not automatically install OPC Core Components; the application still installs or repairs them on demand. An old copy extracted under Downloads or another private-user directory is not migrated—do not keep launching that copy.

If the installation registration remains but its directory or `Uninstall.exe` is missing, setup shows the previous path and lets you choose a directory. Select the old path to repair program files, the uninstaller, and missing shortcuts, or select a new empty path; after a successful install, the registration and installer-created shortcuts point to the new path. Files in the old directory are neither deleted nor moved. Manual registry cleanup is unnecessary. A normal uninstall removes DComEasy's installation registration; if the old directory was deleted manually, the uninstaller cannot run and this repair flow handles the leftover registration.

The Desktop shortcut is created on the all-users Desktop. Uninstall removes it only if it still matches the shortcut created by setup; a shortcut replaced or modified later is retained.

The interface supports Simplified Chinese and English. The initial selection follows the Windows interface language. You can change it in the sidebar, and the application remembers your choice. Switching languages does not clear inputs or unapplied changes, or repeat diagnosis or connection testing.

The license page and startup expiry reminder display the deadline date only (`yyyy-MM-dd`). Actual expiration checks retain their original time precision.

Drag the title or blank area at the top of the window to move it. The top-right controls minimize, maximize/restore, or close the window. Inputs, buttons, and tables are not drag regions and retain their editing, clicking, and text-selection behavior.

## Configuration diagnosis

The application opens on **Diagnostics** without running an inspection automatically. Click **Run Check** to load or refresh the results. No OPC username or password is required. Run a diagnosis before applying configuration.

Diagnosis covers:

- The account running the assistant, which may differ from the Windows desktop user after elevation.
- DCOM default properties, default protocols, and role permissions.
- OPC Core Components, OPCEnum, OPC Automation DLLs, and registration status.
- OPCEnum AppID mapping, application access/launch/activation ACLs, and authentication settings. Application, machine-registry and Windows system defaults are identified separately; listed rules do not establish effective access for a remote caller.

Diagnosis reads local state without applying settings or starting services. Repeating diagnosis preserves unapplied edits. The application warns about remaining unapplied changes when exiting.

The main table shows diagnostic findings: missing OPCEnum AppID mappings, empty/unrestricted DACLs and read failures remain visible. Open Details for ordinary configuration reference, including allow/deny rule counts, authentication level, full sources, SIDs and selectable SDDL. No remote-identity or authentication placeholders are added without evidence. Reference material is excluded from local check counts and exported in separate appendices; they do not establish remote connectivity.



## OPC user

Enter a local OPC username and password on **Configuration**. The visibility button inside the password field toggles plain-text display. Validation runs once when you leave the fields or press Enter in the password field. Complete saved credentials are also validated when the window opens. The status icon shows the result; click it or press Enter to retry with the current inputs. Right-click the status text to view or copy the full diagnostic.

- **Existing user**: the supplied credentials are validated automatically. An incorrect password produces error 1326 and full diagnostic details in the status area. The existing password is not overwritten, reset, or changed.
- **Missing user**: once automatic validation confirms that the local user does not exist, **Create user** becomes available in the **Manage user ▾** menu; creation requires confirmation. New local OPC accounts created by DComEasy have passwords that never expire. Applying DCOM configuration does not implicitly create a user.
- **Saved credentials**: successfully validated credentials are stored through Windows Credential Manager. A failed password validation retains only the username, not the incorrect password.
- **User management**: open the **Manage user ▾** menu. It always shows **Create user**, **Delete local account…**, and **Clear credentials**; **Create user** is enabled only after validation confirms that the local account is missing. **Clear credentials** only clears the inputs and stored credentials. **Delete local account…** works only for local OPC users created by DComEasy. It confirms the account name and SID before deletion; you can then recreate the user from the menu with the current inputs. The recreated account gets a new SID, so existing DCOM permissions and file access may need to be configured again.

Changing either credential clears the previous validation result. Validation runs automatically after input is complete. Unchanged inputs are not retried repeatedly, avoiding excessive Windows logon attempts. An existing account, incorrect password, or disabled account leaves **Create user** visible but disabled. Validation does not overlap with another operation. Right-click the status text to view or copy the full diagnostic.

Accounts created by an older DComEasy release may be subject to the Windows maximum password age. After upgrading, open PowerShell as administrator in the DComEasy installation directory. Run `powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\tools\Repair-DComEasyOpcUser.ps1 -UserName <account>` to inspect the account, then add `-Apply` to repair it once. The script accepts only local accounts marked as created by DComEasy. It preserves the account and password, then checks the SID, password change time, and expiry state. Click the status icon to validate again afterward. Have an administrator inspect other accounts in Windows user management.

## Apply configuration

DCOM default properties and permissions are machine-wide settings, not a separate configuration saved for each logged-in user. The permission table grants operations to the corresponding users or groups; connection testing uses the specified OPC user's identity.

### DCOM permissions

The permission table covers four groups corresponding to Windows COM Security settings:

| Permission type | Settings | Available rights |
| --- | --- | --- |
| Access permissions | Edit Limits, Edit Default | Local Access, Remote Access |
| Launch and activation permissions | Edit Limits, Edit Default | Local Launch, Remote Launch, Local Activation, Remote Activation |

**Diagnostics** uses status icons to show existing rights; **Configuration** uses blue checkboxes to edit selections, with user/group and status columns describing the current configuration. Checkbox color alone does not identify a newly proposed change; review **Preview changes** for that distinction. Gray dashes indicate unavailable choices. Click a permission-column header to select or clear its applicable items.

Selecting a right retains or adds its Allow permission. Clearing an existing selection removes its Allow permission when applied. Select the rights your environment needs; all roles and permissions do not need to be enabled.

### Default authentication level

The initial choice is **Keep Current**, which leaves the existing level unchanged. Available choices include None, Connect, Call, Packet, Packet Integrity, and Packet Privacy. The level is written only when you explicitly choose another setting.

### Default protocols

The list includes configured and system-available protocols. Select the protocols to enable and drag a protocol's name row to change priority. A moving row preview and insertion indicator provide feedback during dragging.

Keep at least one protocol selected. Applying configuration writes the chosen protocols in their selected order; deselecting a configured protocol removes it from the configuration.

### Confirmation and results

Click **Preview changes** to read the current configuration again and list actual changes from your selections without opening a confirmation or writing to the system. Unchanged DCOM permissions and default protocols stay out of the plan; with no edits, the preview shows that no changes are needed. To install or repair OPC components, start OPCEnum, configure the default protocol, or register DLLs, select **Include environment repairs** first. **Apply** recalculates the plan using the same choice and performs no writes when there are no planned changes. Review and confirm a nonempty plan before execution. Results show each step's success, failure, skipped state, or recovery outcome.

A failed operation does not mean all earlier changes were rolled back. Review the current stage, elapsed time, and operation log, then use the inspection results to determine any further action.

## Component deployment and OPCEnum

When OPC Core Components are missing, outdated, or have damaged registration, the application uses the bundled OPC Foundation 3.1.4.132 installer for silent installation, upgrade, or repair as needed. The installed product appears in the Windows installed-apps list.

Applying configuration starts OPCEnum if it is stopped, waits up to 30 seconds, and checks its actual running state. If only a service start is needed, the application does not reinstall the components or additionally change the service to automatic startup. A failed start reports the Windows error or timeout reason.

If the installer requires a restart, the application retains a reminder without restarting the computer automatically; connection testing remains independently available. Apply configuration again after restarting to verify the service state. MSI installation is not forcibly terminated merely because it takes a long time; detailed installer logs are available in `%ProgramData%\DComEasy\Logs`.

If an existing OPC Automation DLL has the same name but different contents from the bundled version, its replacement is included in the configuration confirmation. After confirmation, the application backs it up, replaces it, registers it, and verifies the result. DLL registration has a timeout safeguard.

## Connection testing

1. Provide valid OPC user credentials.
2. On **Connection**, enter the target host and check port. Select the search icon beside ProgID to query OPCEnum on this computer or the specified host as the validated OPC test account. Discovery only refreshes the candidates; it does not open the list or fill any field. The separate arrow only opens existing candidates and never starts discovery. Selecting a server then fills ProgID and CLSID, while ProgID remains directly editable. CLSID takes precedence when both are supplied. If no server is found, the application reports that no registered OPC DA Server was discovered. DA 1.0/2.0/3.0 registration categories and the version used by a successful connection are written to the log instead of being repeated in the list.
3. Start the test and review the latest result, reason, and suggested action.

Examples in empty fields are placeholders only. They disappear on focus and are never submitted as actual parameters.

The test button is available whenever the application is idle; missing credentials are explained in the result area on click. Enter user credentials and target parameters to test directly, without running diagnostics or applying configuration first. Each test validates the specified user, checks the network, then performs OPC DA activation and status retrieval under that user's identity. It neither runs configuration diagnostics nor uses existing diagnostic results as a prerequisite. You can edit the parameters and retry after a failure. Local Automation component issues, remote activation failures, and timeouts are reported separately.

Before OPC activation, the test checks DNS, Ping, and the selected TCP port. Each result remains visible. A missing Ping reply does not block the port check because ICMP may be filtered. A failed port check stops OPC activation. The check port does not change the DCOM ports negotiated by Windows.

Success and failure appear in the result area without additional dialogs. Passing local configuration checks does not establish remote connectivity, and a connection test is not continuous data collection.

Each test automatically saves its connection parameters, test user, time, and detailed success or failure result, without passwords. The **Connection history** tab remains available after restarting, and the latest target inputs are restored automatically while preserving saved credentials. Right-click a history row and choose **Restore connection inputs** to reuse that test target. **Delete this record** removes the saved record without changing the current connection form. Switching usernames clears any password belonging to another user. Restoring inputs does not start a test. Records are stored under the current Windows user's `%LOCALAPPDATA%\DComEasy\connection-history`. Node browsing and refreshes do not create duplicate connection-test records. Storage errors appear in the operation log; the result remains available for the current session.

### Browsing and monitoring

A successful connection loads only the first tree level on the left. Expand a folder to query its children. The right-hand monitoring list starts empty. Right-click a point and choose **Add to monitoring**; duplicate ItemIDs are ignored. A folder's context menu adds only its already loaded descendant points, without recursively browsing unopened folders.

The full ItemID query remains available at the top: enter an exact ItemID and press Enter to read it directly and add the point to monitoring, where failed reads are also shown. The current interface does not show a separate **Query ItemID** button. Typing also filters the loaded tree without filtering the monitoring list. **Refresh tree** beside the search field and the refresh icon on the right of the node heading reload the first level while preserving monitored points, values and intervals.

Each monitoring row shows ItemID, value, quality, refresh interval, server timestamp and read errors. Boolean switch values appear as 0 or 1. Scroll horizontally to view all columns. Monitoring and connection-history cells support dragging to select text and copying with Ctrl+C. Monitoring also offers the **Copy** context-menu action. The fixed leftmost checkbox column selects points for batch actions; its header checks or clears all points. Text selection is for copying. New points start unchecked with polling off; unchecking does not stop existing polling. Right-click an unchecked point to set its interval directly, or right-click a checked point to act on all checked points. Choose a preset, disable polling, or set a custom 1–3600 second interval. **Read once** performs one read without enabling polling. **Select all** in the context menu checks every point. Right-click active points and choose **Stop monitoring** to stop only the selected points while retaining their rows and last values. Other points continue reading; late results for stopped points are ignored. Set a positive interval to resume. **Remove selected monitors** or Delete removes points and stops future polling.

Automatic polling reads only enabled monitored points and pauses away from the node page or when hidden. Requests run sequentially in the background, preserving selection, scrolling and toolbar button states while the page remains interactive. Manual queries, tree refreshes and reads take priority by cancelling the pending automatic request first. Failed reads show per-point errors; bad and uncertain quality remain explicit.

Changing the target or credentials clears the tree and monitoring session; test again to use the new target. Monitoring selections and intervals are session-only. Node operations do not overwrite saved connection-test results. Each directory query is limited to 10,000 direct children, a bounded result size and a timeout; partial results are indicated. Long values and large arrays are truncated for display.

## Multi-point monitoring tasks and trend reports

**Monitoring tasks** provide long-running collection for multiple items on one OPC DA server. Choose **Add to monitoring task…** from the node browser or monitoring list, or create a task on the task page. A monitoring-list action uses all checked rows when the context row is checked; otherwise it uses only that row. Duplicate ItemIDs are removed, and adding points never starts trigger detection.

A task reads 1–64 points at one shared integer interval from 1 to 3600 seconds. Every round uses one batch read on one OPC Group. Client sample time aligns the common trend axis; the original OPC timestamp is retained unchanged. Repeated server timestamps are not errors. Boolean switch values display and plot as false=0 and true=1, and can be used by numeric threshold rules; the raw type remains Boolean. A failed or bad-quality point becomes a gap without replacing its value, while the other points in that round remain available.

The **New task** dialog asks only for a name and saves an empty task. Use **Configure** on its row after creation to add points and set the interval, trigger rule and output folder. Creating from a point context menu still carries the selected points, without showing configuration fields during creation. Saving, loading and adding points never starts a task; application restart does not resume tasks. Connection and OPC credentials come from the existing Configuration and Connection test pages, not separate task inputs. Starting captures a fixed connection and identity; later page edits do not change that run. The server must match the task point source.

**Add points** automatically tests the configured server and credentials, then opens its node tree; no separate manual connection test is required. Branches load on expansion, and tags can be selected across branches. Left-click a tag name or checkbox to toggle it; right-click copying leaves checks unchanged, and branches cannot be sampled. Existing tags are marked and cannot be added again; a task accepts up to 64 tags. A server mismatch produces a prompt without switching servers. Connection failures show the reason, stage, error code and guidance in copyable text, without stack traces. The point table has checkboxes, a select-all header and consecutive row numbers starting at 1. **Remove points** removes checked tags only; text selection remains available for copying. **Set trigger point** uses the current row; removing that tag clears the selection. Interval and pre/post fields accept direct text entry without spinner arrows, with hover help for the supported integer ranges. Invalid input shows a copyable field/range message and blocks saving until corrected.

Enable the numeric trigger rule, select a trigger tag from the task, and set a valid comparison and threshold before using **Start** on the task row. An incomplete rule disables Start; hovering explains what is missing. A running task collects and checks all points at the shared interval across page changes, minimization and hiding, after the report folder passes preflight. **Trends** remains available without a rule: it temporarily collects all task tags without starting the task or generating reports. **Stop** ends collection and detection while retaining recent trends. Restarting creates a fresh buffer. During start preparation, queueing and collection, configuration changes, adding/removing points, deletion and duplicate starts are disabled. Trends, sample details and event reports remain viewable, and Stop remains available. Stop the task before editing its configuration.

Numeric rules support `<`, `≤`, `>`, `≥`, and `=`. Equality compares valid numbers exactly. A matching first sample triggers once; sustained matches do not repeat until a valid nonmatch arrives. Failed and bad-quality reads neither trigger nor re-arm. A new match during an earlier post-trigger window creates a separate overlapping event.

A failed preflight restores the prior idle/stopped state and retains a copyable error without opening an acquisition session or updating the task start time. It does not enable Stop; faults after real acquisition still support stopping. The trend tabs use concise captions, **Live Trends** and **Samples**, without changing the shared time axis or latest-1000 sample limit.

Each pre/post window accepts 0–60 seconds. New tasks default to 30 seconds on each side. Legacy windows above 60 seconds load as 60 seconds without losing tasks; source files remain unchanged until saved. If a run started too recently, contains read gaps, or exits early, only real samples are saved and the shortage is identified—no samples are fabricated. Live trends and PDF overlay all tags in one chart with shared time and value axes and distinct colors. Sample markers are thicker than lines. The PDF point list carries the curve-color key; the live chart has no persistent legend. The live chart defaults to the latest minute; the range selector beside its heading immediately switches between one and five minutes without reconnecting or clearing samples. Rule-enabled tasks retain at least five minutes of recent trend data. Hovering near any sample shows the client sample time and every task tag's value or failure status for that round; single-tag tasks use the same format. Each hover row shows the tag name and its curve-color marker. The chart has no inline labels or unrelated details over empty areas. The PDF uses time labels on the shared axis only and adds numeric labels beside sparse samples where they do not collide. Its sample-value summary shows the trigger round and up to three actual rounds on each side, listing every tag's value or failure status below the chart or on continuation pages; missing rounds are never invented. The chart still marks the trigger and threshold; CSV holds the complete samples. CSV contains one row per tag per round, including client sample time, value, quality, original OPC timestamp, and complete read error.

Output is archived as `output/task name/trigger time/监测报告.pdf` and `采样数据.csv`. Invalid Windows filename characters are sanitized. Trigger directories use local time to the second; a collision adds milliseconds, then a sequence number if needed, without overwriting earlier reports. Configuration rejects archive names occupied by another task or existing file/directory, while an already configured task can reuse its archive. No ownership markers, event reservation files or temporary report files are created. A failed generation retains the event snapshot and any completed file for retry. Tables and full errors support selection, Ctrl+C, and context-menu copying.

The page header contains only **New task**; the task-list card has **Refresh tasks** at the right of its heading. Refresh rereads task and report records from disk, synchronizing idle task additions, edits and deletions and the report count. If a running task's file was externally deleted, refresh leaves acquisition intact; stop it and refresh again to remove its row. A damaged task file shows a copyable reason instead of causing a partial read to remove tasks. Each row has five icons: Configure, Trends, Start, Stop and Delete, with action names on hover. Actions target that row; use Left/Right and Enter for keyboard access. **Configure** manages points, sampling and rules; stop before editing. **Trends** always opens live data for all tags. Idle tasks use temporary acquisition without changing task start state, evaluating rules or generating reports; closing the window stops temporary acquisition. Running tasks reuse their existing samples without opening another acquisition session. Starting, stopping or editing a task switches the view's data source accordingly. Empty tasks prompt to add tags; connection failures provide copyable errors and a retry action. The sample tab displays the latest 1000 rows; full event samples remain in CSV. Pausing view updates does not pause collection.

Sample details label the first column **Time** and show the original OPC timestamp in local `yyyy-MM-dd HH:mm:ss.fff` format. They omit the client sampling time column; missing OPC timestamps stay blank rather than being replaced by client times. Client sampling times still align the chart and remain in CSV. Sample columns resize with the window to avoid horizontal scrolling. Hovering over a long read error shows its full text, and selecting its cell allows Ctrl+C or right-click copying of the complete content. The pause/resume action at the right of the trend heading is a 40×40px blue button with a white 22px icon, scaled for DPI. It controls view updates only, with a hover hint; resuming immediately displays the latest samples. The sample status sits inside the bottom of the trend card, aligned with the content and padded vertically. Complete errors remain scrollable, selectable and copyable.

Collection, Last trigger and Error details columns are removed. Actions are last; column widths adapt to the page, with point counts and intervals centered. **Task started** shows the actual start time, which remains after stopping and updates on restart. A task without a trigger rule cannot start, but Trends can still temporarily collect samples. **Reports** counts completed reports and opens the actual task archive, offering a directory picker and copyable list for multiple archives. Zero opens nothing. Failed reports can be retried from the context menu; **View error details** and **Copy error details** retain full diagnostics without a table column. Deleting removes configuration only, not reports.

The destination picker uses checkboxes to add selected points to multiple same-server tasks, deduplicating each task independently. Running tasks cannot be checked. A failed destination does not prevent other saves; failures appear in one copyable summary. All curves share one plotting area; adding tags does not add subplots. Connection-test polling follows fixed dispatch slots and displays responses immediately. Slow reads never overlap or cause catch-up bursts; communication and UI scheduling may still delay actual dispatch.

Starting detection checks that the output folder is writable. Stopping or exiting with unfinished events prompts before saving partial reports marked with a short post-trigger window. Persisted pending reports resume on the next launch without resuming detection. Failed snapshot writes retain their data in memory and must be retried successfully before exiting. At 32 failed snapshot writes, new trigger detection stops while collection continues to prevent unbounded memory growth. The rolling buffer is bounded according to point count, interval and event-window length; large configurations require more memory.

## Network checks and local port rules

**Network** works without OPC credentials. Enter a host and port, then click **Check** to see Ping, target TCP access, local TCP/UDP listeners, active firewall status, and a TCP rule summary. Results usually take six rows; multiple active networks have separate firewall rows. DNS appears only on failure. Rules are counted only when enabled, inbound, and matching the active network and port. Individual rules are not listed. Issues retain useful details and hints. **Scope** separates target checks from local information. Remote firewall settings are not read.

Under **Local ports**, enter a port and select TCP or UDP. Use **＋ Add port** for more rows, select the rows to apply, then click **Open selected ports** to run the batch immediately. The initial row is TCP 135; new rows are selected by default and can be removed. Rules always use the current local network. All selected rows are validated before any write. Duplicate port/protocol pairs are merged. Each inbound allow rule is verified after saving; identical rules are reused and conflicting names are not overwritten. A failed item does not stop later items. Results show the latest batch, with added, existing, and failed counts. The service must still be listening.

An allow rule does not start a service or override block rules or domain policy. **Rule saved** confirms the stored rule; use listener and connectivity checks to verify access.

## Import and export encrypted configuration templates

Pro and Enterprise can export the current values on the **Configuration** page as an encrypted `.dc` file for use on another computer. Export captures the page draft; the source computer does not need to have applied or validated it. The template includes the username, password, default authentication level, DCOM permissions, protocol order, and the environment-repair option. Connection-test hosts, ProgID, CLSID, probe ports, connection history, and RPC port settings are excluded.

1. Review the current **Configuration** page, switch the right-hand card to the **Configuration templates** tab, click **Export configuration**, and save the `.dc` file. No additional password is required.
2. On the target computer, switch to **Configuration templates**, click **Import configuration**, and open the `.dc` file. Import is accepted only when the file's configuration fields exactly match the current client's configuration schema; there is no user-selectable V1/V2 file version.
3. Import fills the page draft and does not change the system immediately. The imported username and password remain editable, and the final entered values take precedence. If the username does not exist locally, DComEasy displays it and asks whether to create the account first. A created account remains even if the later configuration is cancelled or fails.
4. Use **Preview changes** to review the operations, then use **Apply configuration**. If an operation fails, DComEasy continues attempting to roll back earlier reversible changes and shows both execution and rollback results in copyable details. Irreversible steps such as component installation are identified separately.

DComEasy encrypts each `.dc` file and verifies its integrity automatically. A damaged or modified file is rejected, and no separate password is required. The template still contains sensitive credentials that can be used to create or configure a local account, so store and transfer it only through trusted channels.

## Export diagnostic reports

After diagnosis, click the export icon at the top right of **Diagnostics**. Hovering over the icon displays **Export report**.

1. Choose a report format. The current release can export PDF or HTML without a watermark. PDF is selected by default each time.
2. Choose a destination and filename. Replacing an existing file requires confirmation.
3. A brief notification appears at the top of the page after export, and the saved path is recorded in the operation log. The report is not opened automatically.

The report uses the most recently completed diagnosis, including its timestamp, computer, application version, application user, basic settings, DCOM role permissions, and default protocols. It is not live state or a connection test result. Passwords, credentials, raw logs, and unapplied selections are excluded.

PDF reports use landscape A4 pages with selectable, copyable text, an embedded Chinese font, and repeated table headers across page breaks. HTML reports are self-contained files. Both formats use the interface language at export time. Export is unavailable before diagnosis completes or while another operation is running.

## Logs and backups

| Content | Location |
| --- | --- |
| Operation logs and detailed MSI logs | `%ProgramData%\DComEasy\Logs` |
| Binary backups, restore targets, and SHA-256 information | `%ProgramData%\DComEasy\Backups` |

The **Connection log** area at the bottom of **Connection** shows copyable connection-related information. **Clear log** clears the displayed content. The current interface does not show the former bottom-right toggle for the shared operation-log panel. Log files remain available in the directory above.

Before applying configuration, the application checks that the log directory is writable. A logging failure after a configuration write is reported separately; it does not misrepresent completed changes as unapplied.

When closing the window, you can choose to minimize or exit and remember that choice. There is no separate close-behavior setting in the sidebar.

## Release files and licensing

The installed program directory contains `DComEasy.exe`, `DComEasy.OpcRuntime.*.msi`, OPC Automation DLLs, and runtime dependencies. Launch the installed version from the Start menu; do not move or copy only its EXE. Uninstalling DComEasy leaves license state, ProgramData logs and backups, per-user connection history, and separately installed OPC Core Components in place.

The client always enforces offline licensing. An unactivated installation uses the Free edition; activation codes enable the features assigned to Pro or Enterprise. Deployment sites do not need internet access, and the License page shows the edition, license ID, and usage period.

Product license files are `LICENSE.txt` and `LICENSE.en.txt` in the release root. Third-party notices are in `notices`, including `notices/opc-core-components.md` for OPC Core Components.

Full product license in this repository: [English](licensing/LICENSE.en.txt) · [中文](../LICENSE).

When a ProgID is supplied, remote OPCEnum resolves the actual CLSID before direct OPC DA activation. An explicit CLSID connects directly. Connection and node operations no longer use the legacy OPC Automation wrapper.
