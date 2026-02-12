# Introduction

## Latest CLI Version

The latest CLI release version: ![Latest Release](https://img.shields.io/github/v/release/EENCloud/EEN-CLI-Public)

## Using the CLI

## Setting-up of Executable File

- Extraction of file from a compressed file format

  #### **In Linux:**

  - There are multiple ways to extract a file from a compressed file. Here are the step-by-step instructions:

  - First method:

    1. Point the cursor on the compressed file.
    2. Right-click on it to trigger the context-menu (right-click menu).
    3. On the context menu select the `Extract Here` option to extract the file in the same directory or
       Select the `Extract to` option in order to extract the file into the current directory or directory of your choice.

  - Second method:

    1. Point the cursor on the compressed file.
    2. Left-Double-click on it to trigger a window that shows the extraction option.
    3. Select the `Extract` button to extract the file into the desired directory.

  - Third method:
    1. Open the terminal in the directory where the compressed file is stored.
    2. Type in the terminal command `unzip een.zip` to extract the file in the current directory.
    ```
    unzip een.zip
    ```

  #### **In Windows:**

  - Here are the step-by-step instructions:
    1. Point the cursor on the compressed file.
    2. Right-click on it to trigger context-menu(right-click menu).
    3. On the context menu select `Extract All`.
    4. A window is triggered that shows an input box which is used to insert the directory path to a chosen directory.
    5. After choosing a directory click on the `Extract` button, to extract the file to the chosen directory.

<br/>

#### Notes:

- For all commands with `--prompt` option will show user confirmation prompts. This means it will show confirmation message when overwriting any existing files.
- Open all the CSV file outputs in Google Sheets or Libre Office as Excel has formatting issues.
- `verbose mode` : Use `--verbose` along with the commands to access the verbose mode.
- All time inputs should be of the format `YYYYMMDDhhmmss.sss (20230125062511.000)`
- Execute this extracted file by mapping up the directory path of the een on the terminal
- Each command should start with `./`.

  Examples:

  ```
  een --version
  ```

- To check if the executable works fine

  - Run the command:

  ```
   een
  ```

  - Output:

  ```
  v<version number>

    usage: een [-v | --version] [-h | --help] <object> <command> [<args>]

    These are common een commands used in various situations:

    auth login              login to the account
    auth logout             logout of the account

    camera list             list all cameras
    camera status           list status of all cameras

    bridge list             list all bridges
    bridge availability     get bridge availability

    'een help' lists all the commands and options
    'een <command> help' lists the usage with options and descriptions
  ```

# EEN Command Line Interface Manual

## NAME

`een` - A command-line tool for managing and retrieving information related to cameras, bridges, users, and more in a cloud-based environment.

## SYNOPSIS

```
een [OPTIONS] <object> <command> [ARGS]
```

## DESCRIPTION

The **een** CLI provides various commands to interact with cameras, bridges, users, sites, and other resources. It offers multiple options for fetching information in different formats (CSV, tree structure, etc.) and supports both standard and v1 APIs.

#### Options:

- **--help, -h**
  Displays the help information for the een command or a specific object.

- **--version**
  Displays the current version of the een CLI.

## COMMANDS

### Version

```
een --version
```

Displays the version of the een tool.

### Help

```
een help
```

Shows detailed help instructions. For shorter help on a specific object, use:

```
een <object> --help
```

## General Options:

General options are available for all commands that include `[general-options]` in their usage.

- `--call-time`
  Display api response time.
- `-d, --debug`
  Display detailed debug output.
- `-h, --help`
  Display how to execute the selected subcommand and provides usage examples.
- `--prompt`
  Display user confirmation prompts.
- `--time`
  Display time taken to execute the command.

Note: `--prompt` may be unavailable for some commands.

## EXAMPLES

```
een help
een --help
een -h
een auth --help
een camera list --help

```

### Time

Shows the execution time of the command, use:

```
een <object> [COMMAND] [options] --time
```

### Call Time

Shows the time taken to get response from api, use:

```
een <object> [COMMAND] [options] --call-time
```

# auth - Manage EEN auth

## NAME

`auth` – EEN authentication commands

## SYNOPSIS

```
een auth [COMMAND] [options]
```

## DESCRIPTION

The **een auth** command provides utilities for logging in and out of Eagle Eye Networks. When using `auth login`, the user is redirected to a login URL and completes the authentication in the web browser. However, when the `--v1` option is used, the user is authenticated directly through the CLI.

## COMMANDS

### login

Log in to EEN using the provided credentials.

#### Usage:

```
een auth login [options] [general options]
```

#### Options:

- `-p, --password <password>`
  Password for login. Use quotes around the password if it contains special characters (e.g., `--password "MyP@ssw0rd!"`).
- `-u, --username <username>`
  Username for login (e.g., `--username admin@example.com`).
- `--v1`
  Use the v1 API for authentication.

#### Notes:

- If the shell misinterprets special characters, ensure the password is wrapped in quotes.

---

### logout

Log out of your EEN account.

#### Usage:

```
een auth logout [general options]
```

## EXAMPLES

- To login

```bash
een auth login --username johndoe --password secret --debug
```

```bash
een auth login
```

- To logout

```bash
een auth logout --debug
```

---

# user - Manage Users

## NAME

`user` - manage and interact with users.

## SYNOPSIS

```
een user [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `user` command allows you to manage users, list user permissions, and export user data in various formats.

## COMMANDS

### list

List users.

#### Usage:

```
een user list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--html`
  Generate a chart in an HTML file; ensure that the --v1 option is used.
- `--include [value1, value2]`
  Display associated items (supported values: email, firstname, id, lastname, permission, status).
- `-l, --long`
  Display details of user including accessible cameras, language, last login, login status, permissions.
- `--v1`
  Use v1 APIs.

#### Selectors:

- `--email [email-id1, email-id2]`
  Filter by email ID.
- `--firstname [first-name1, first-name2]`
  Filter by first name.
- `--id [id1, id2]`
  Filter by user ID.
- `--lastname [last-name1, last-name2]`
  Filter by last name.
- `--status [status1, status2]`
  Filter by status (supported values: active, pending, blocked).

#### Actions:

- If `--html` is specified, generate a user permissions report.
- If `--csv` and `--v1` are both specified, export users in CSV format using v1 APIs.
- If `--csv` is specified, export users in CSV format.
- If `--google-sheet` is specified, export and upload user data to Google Sheets.
- If `--v1` is specified, list users using v1 APIs.

## EXAMPLES

- To list all users:

```bash
een user list --header --csv
```

#### Output

```csv
"id","account id","first name","last name"
"ca046095","00052029","Anandhakrishnan","M"
"ca01060e","00052029","Anandhan","Sreekumar"
```

- To list users in CSV format:

```bash
een user list --csv -f users.csv
```

- To generate an HTML report of user permissions:

```bash
een user list --html
```

---

### set

Update user settings.

#### Usage:

```
een user set [parameter] [value] [options] [selectors] [general options]
```

#### Parameters:

- `firstname <first-name>`
  Update first name.
- `lastname <last-name>`
  Update last name.
- `permission <permissions>`
  Update permission.
- `status`
  Enable or disable a user.

---

### set firstname

Update the first name of users.

#### Usage:

```
een user set firstname <first-name> [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `--email [email-id1, email-id2]`
  Filter by email ID.
- `--id [id1, id2]`
  Filter by user ID.

#### Example:

```bash
een user set firstname "John" --email "user@example.com"
```

---

### set lastname

Update the last name of users.

#### Usage:

```
een user set lastname <last-name> [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `--email [email-id1, email-id2]`
  Filter by email ID.
- `--id [id1, id2]`
  Filter by user ID.

#### Example:

```bash
een user set lastname "J" --email "user@example.com"
```

---

### set status

Activate or block users.

#### Usage:

```
een user set status [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `--disable`
  Disable user
- `--enable`
  Enable user
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `--email [email-id1, email-id2]`
  Filter by email ID.
- `--id [id1, id2]`
  Filter by user ID.

#### Examples:

- To enable users by ID:

  ```bash
  ./een user set status --enable --id 'ca020825, ca04fb15' --header
  ```

#### Output

When running `een user set status --enable --id 'ca020825, ca04fb15'` command with `--csv` and `--header`, the output will be in CSV format suitable for scripting and automation.

**Successful Output Example:**

```csv
Updated user details for 2/2 users

"user id","email","first name","last name","is successful"
"12345","alice@example.com","Alice","Johnson","yes"
"12346","bob@example.com","Bob","Doe","yes"
```

**Error Output Example:**

```text
Updated user details for 1/2 users

"user id","email","first name","last name","is successful","error reason"
"12345","alice@example.com","Alice","Johnson","yes",""
"12346","bob@example.com","Bob","Doe","no","user is already active"
```

---

### set permission

Update user permissions.

#### Usage:

```
een user set permission <permissions> [options] [selectors] [general options]
```

#### Arguments:

- `permissions` — supported values:
  `viewVSP`, `editMap`, `talkDown`, `editUsers`, `controlPTZ`, `editSharing`, `exportUsers`, `viewArchive`, `editArchive`, `viewVSPRule`, `editVSPRule`, `editAccounts`, `viewAuditLog`,
  `editSpeakers`, `viewLiveVideo`, `administrator`, `createLayouts`, `downloadVideo`, `upgradeEdition`, `addEditSpeakers`, `viewVehicleList`, `editVehicleList`, `viewAutomations`,
  `editAutomations`, `editPTZStations`, `editMotionAreas`, `viewPreviewVideo`, `turnCamerasOnOff`, `viewHistoricVideo`, `layoutAdministrator`, `editAllCameraSettings`,
  `addEditBridgesCameras`, `editNoBillingDeviceSettings`.

#### Options:

- `--csv`
  Display details in CSV format.
- `--disable`
  Disable permission.
- `--enable`
  Enable permission.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `--email [email-id1, email-id2]`
  Filter by email ID.
- `--id [id1, id2]`
  Filter by user ID.

#### Examples:

- To enable permissions for users by ID:

  ```bash
  ./een user set permission 'editMap,viewVSP' --enable --id 'ca020825, ca04fb15' --header
  ```

---

# account - Manage User Accounts

## NAME

`account` - manage and interact with user accounts.

## SYNOPSIS

```
een account [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `account` command allows you to manage reseller accounts, list all accounts, and switch between sub-accounts.

## COMMANDS

### list

List all logged-in accounts.

#### Usage:

```
een account list [options] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items (supported values: id, name).
- `-l, --long`
  Display details of account, including account ID, account name, and account type.
- `-s, --sub-account`
  Display sub-accounts (only applicable for reseller accounts).

---

### switch

Switch to an account.

#### Usage:

```
een account switch [options] [general options]
```

#### Options:

- `-a, --account-id [account ID]`
  Specify account id to switch to.
- `-s, --sub-account-id [sub-account ID]`
  Specify sub account id to switch to.
- `--username [username]`
  Specify username to switch to.

## EXAMPLES

- To list all accounts of the reseller:

```bash
een account list --header
```

#### Output

```text
"account"
"Sijin Jacob(00052029)"
"Deepak M K(00064711)"
```

- Switch to a sub-account (from reseller account):

```bash
een account switch --sub-account-id <sub-account ID>
```

- Switch back to reseller account (from sub-account):

```bash
een account switch
```

- Switch between different logged-in accounts:

```bash
een account switch --account-id <account ID>
```

## Notes:

- When you're logged in as a reseller and want to access a sub-account, you must use the `-s` flag with the sub-account ID.
- To switch back to the reseller account from a sub-account, run `een account switch` without any options.
- The `-a` and `--username` options are for switching between different accounts you're logged into, not for sub-account switching.

---

# archive - Manage Archives

## NAME

`archive` - manage and interact with archives.

## SYNOPSIS

```
een archive [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `archive` command allows you to manage archives, including listing archives and downloading specific archives.

## COMMANDS

### list

Get the list of available archives.

#### Usage:

```
een archive list [options] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-D, --detailed`
  Display detailed archive list.
- `--header`
  Display column headers in the result.
- `-l, --long`
  Display archive details, including file name, size, creation date, shared status, and shared path.
- `-t, --target-directory [target directory]`
  Specify the directory from which the archive will be retrieved.

---

### download

Download a specific archive.

#### Usage:

```
een archive download <archive> [options] [general options]
```

#### Arguments:

- `<archive>`
  The name of the archive to download.

#### Required Options:

- `-t, --target-directory [target-directory]`
  Specify the name of the directory to save the output.

#### Options:

- `-o, --overwrite`
  Specify whether to overwrite already downloaded archive.

## EXAMPLES

- To list available archives:

```bash
een archive list --detailed --csv --target-directory /path/to/output
```

- To download a specific archive:

```bash
een archive download <archive> --target-directory /path/to/save --overwrite --debug
```

---

# auditlog - Manage Audit logs

## NAME

`auditlog` - Manage audit log.

## SYNOPSIS

```
een auditlog [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `auditlog` command allows you to list audit log.

## COMMANDS

### list

List audit logs.

#### Usage:

```
een auditlog list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in Google Sheets.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items (supported values: user, audit-type, description).
- `-l, --long`
  Display details of audit log including user id, target type, target id, account id.

#### Selectors:

- `--audit-type [audit type]`
  Filter by audit type (supported values: notificationSent, notificationNotSent, create911Camera, createAction, updateAction, deleteAction, reportCreated, reportDeleted, createReportSchedule, deleteReportSchedule, updateReportSchedule, createRegister, updateRegister, deleteRegister, createAlert, clearAlert, getLayout, createLayout, deleteLayout, updateLayout, addPosSystem, updatePosSystem, deletePosSystem, createFile, deleteFile, updateFile, createLocation, updateLocation, deleteLocation, lprSearch, videoSearch, searchTransaction, bridgeSwap, createLprRule, updateLprRule, delteLprRule, createSensorGateway, deleteSensorGateway, updateSensorGateway, createSensor, deleteSensor, updateSensor, createRule, updateRule, deleteRule, createVehicleListEntry, updateVehicleListEntry, deleteVehicleListEntry, newVehiclesAdded, vehiclesDeleted, existingVehiclesUpdated, updateMeasurement, createRole, updateRole, deleteRole, createVehicleList, updateVehicleList, deleteVehicleList, createUserViaApplication, createUserViaSso, deleteUser, updateUser, userLogin, userLogout, forgotPassword, resetPassword, userSettingsSnapshot, updateUserRole, assignRoleToUser, unassignRoleToUser, acceptedTermsAndConditions, grantResourceToUser, ungrantResourceToUser, createMeasurementThreshold, deleteMeasurementThreshold, updateMeasurementThreshold, requestDownloaded, saveDownloaded, videoRecordStart, videoRecordEnd, viewVideoStart, viewVideoEnd, createExport, createGroup, updateGroup, deleteGroup, groupAssignmentRemove, groupAssignmentAdd, bulkCreateGroupAssignments, bulkDeleteGroupAssignments, assignUserToGroup, unassignUserToGroup, createAccount, deleteAccount, updateAccount, switchAccount, accountSettingsSnapshot, activateFirstResponders, deactivateFirstResponders, updateResponderCamera, removeResponderCamera, updateTransaction, createDevice, deleteDevice, updateDevice, devicesOn, devicesOff, deviceRestart, managedSwitchControl, managedSwitchUpdate, deviceSettingsSnapshot, openTunnel, closeTunnel, activeOutput0, activeOutput1, activeOutput2, activeOutput3, cameraSnapshot, audioSessionStarted, audioSessionFinished, createCameraShare, deleteCameraShare, updateCameraShare, cameraSwap, updateCameraAddress, upgradeDevice).
- `-e, --end-time [end time]`
  Filter by end time (defaults to current time).
- `-s, --start-time [start time]`
  Filter by start time (defaults to 10 minutes before the current time).
- `--target-id [target id]`
  Filter by target id.
- `--target-type [target type]`
  Filter by target type (supported values: notification, action, report, posRegister, alert, layout, posIntegration, file, location, analytic, lprRule, sensorGateway, sensor, rule, vehicleListEntry, measurement, role, vehicleList, user, measurementThreshold, video, group, account, posTransaction, device).
- `-u, --user-id [user id]`
  Filter by user id.

## EXAMPLES

- To list all audit logs with headers in CSV format:

```bash
een auditlog list --header --csv
```

#### Output

```csv
"user","type","timestamp","description"
"Lakshmi Sai P(lpaspuleti+vs@een.com)","Create File","2025-10-07T09:43:17.851+00:00","File name "VSP Events Count Summary Report - 20251007094316035.html" created"
"Lakshmi Sai P(lpaspuleti+vs@een.com)","Create File","2025-10-07T09:43:17.461+00:00","File name "VSP Events Count Summary Report - 20251007094316035.csv" created"
```

- To list all audit logs for a specific time with target type file with headers in CSV and long list format:

```bash
een auditlog list -s 20250328010101.000 -e 20250328010204.201 --target-type 'file' --csv --header -l
```

#### Output

```csv
"user","audit type name","timestamp","description","user id","target type","target id","account id"
"Harees Kumar(hkumar+vsp@een.com)","Create File","2025-11-27T06:43:31.466+00:00","File name "Worker Safety Monitoring Report - 20251127064330736.html" created","ca0c6b19","file","00052029","00052029"
"Harees Kumar(hkumar+vsp@een.com)","Create File","2025-11-27T06:43:31.142+00:00","File name "Worker Safety Monitoring Report - 20251127064330736.csv" created","ca0c6b19","file","00052029","00052029"
```

---

# availabledevices - Manage Available Devices

## NAME

`availabledevices` - manage available devices.

## SYNOPSIS

```
een availabledevices [COMMAND] [OPTIONS]
```

## COMMANDS

### list

List of all devices found by the bridges in the account that have not yet been added.

#### Usage:

```
een availabledevices list [options] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `-l, --long`
  Display details of devices, including visibility by bridges, make, model, IP address.

#### Selectors:

- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esn.
- `--devicestate [state1, state2]`
  Filter by device state (supported values: notSupported, addable, inOtherAccount, unknown).
- `--devicetype [type1, type2]`
  Filter by device types (supported values: camera, speaker, display, multiCamera).

## EXAMPLES

- To list all available devices:

```bash
een availabledevices list
```

- To list all available devices for a specific device type with debug option:

```bash
een availabledevices list --devicetype 'camera, speaker' -d
```

---

# camera - Manage Cameras

## NAME

`camera` - Manage camera settings and operations

## SYNOPSIS

```
een camera [COMMAND] [OPTIONS]
```

## COMMANDS

### list

List cameras.

#### Usage:

```
een camera list [options] [selectors] [general options]
```

#### Options:

- `-A, --all`
  Display all cameras, including shared ones.
- `--csv`
  Display details in CSV format.
- `--direct`
  Display cameras which are direct to cloud.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--html`
  Generate a chart in an html file.
- `--include [value1, value2]`
  Display associated items (supported values: esn, camera, bridge-esn, bridge, site, siteid, status, tag).
- `-l, --long`
  Display details of camera, including camera name, camera id, bridge id, bridge name, status, site name, site id, timezone, guid, tags, is shared, is direct, ip address, mac address.
- `--shared`
  Display cameras that are shared.
- `-T, --tree`
  Display cameras and associated bridges in tree format.
- `--v1`
  Use v1 APIs.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

#### Example

To list all cameras with specific fields in CSV format (with headers):

```bash
een camera list --include 'esn,camera,bridge-esn,bridge,site,siteid,status,tag' --header --csv
```

#### Output

```csv
"camera id","camera name","bridge id","bridge name","site id","site name","status","tags"
"12345d7f","Test camera 1","10135b4a","Test bridge - 1","b583ace7-6ee2-450a-9f5a-15a8f7ffcd73","Test Site - 1","deviceOffline","109"
"13345d7f","Test camera 2","10135b4a","Test bridge - 2","b583ace7-6ee2-450a-9f5a-15a8f7ffcd73","Test Site - 2","online","108"
"14345d7f","Test camera 3","10135b4a","Test Site - 2","b583ace7-6ee2-450a-9f5a-15a8f7ffcd73","Test Site - 2","off","110"
```

---

### get

Get camera settings and analytics.

#### DESCRIPTION

The `camera get` command allows you to get a specific setting for one or more cameras.
You can specify the setting to retrieve as `<parameter>`.
You can use selectors (like `--esn`, `--tag`, `--site`, etc.) to target specific cameras.

#### Usage:

```
een camera get [parameters] [options] [selectors] [general options]
```

#### Parameters:

- `audio`
  Get audio settings (Is audio enabled or not).
- `camera-name`
  Get the camera name.
- `password`
  Get the camera password.
- `username`
  Get the camera username.
- `preview-update-rate`
  Get the preview video update rate (in ms).
- `preview-quality`
  Get the preview video quality.
- `preview-resolution`
  Get the preview video resolution.
- `preview-transmit-mode`
  Get the preview video transmit mode (values: onDemand, always, background, event).
- `video-capture-mode`
  Get the video capture mode.
- `video-quality`
  Get the video quality.
- `video-resolution`
  Get the video resolution.
- `video-transmit-mode`
  Get the video transmit mode.
- `cloud-retention`
  Get the cloud retention days.
- `minimum-premise-retention`
  Get the minimum premise retention days.
- `maximum-premise-retention`
  Get the maximum premise retention days.
- `scene-analytics`
  Get scene analytics (Is scene analytics enabled or not).
- `cloud-preview-only`
  Get cloud-preview-only status (If the camera is under CMVR, return "Yes" or "No" depending on whether cloud-preview-only is enabled. If the camera is not under CMVR, return "-" instead of "yes" or "no").

#### Options:

- `--csv`
  Display details in CSV format.
- `--file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheets.
- `--header`
  Display column headers in the result.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by on camera esns.
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `--tag [tag1, tag2]`
  Filter by tags.

#### EXAMPLES

```bash
# Get audio settings
een camera get audio --esn 12345

# Get preview update rate and save as CSV
een camera get preview-update-rate --bridge-esn 12345 --csv -f update-rate.csv

# Get scene analytics for all cameras and export to Google Sheets with headers
een camera get scene-analytics -g --header
```

#### Output

When running a `camera get audio` command with `--csv` and `--header`, the output will be in CSV format and is suitable for scripting and automation.

```
"camera id","camera name","is audio enabled"
"10062dd9","0000","no"
```

---

### set

Edit camera's settings.

#### DESCRIPTION

The `camera set` command allows you to update a specific setting for one or more cameras.
You can specify the setting to change as `<parameter>`, and the new value as `<value>`.
You can use selectors (like `--esn`, `--tag`, `--site`, etc.) to target specific cameras.

#### Usage:

```
een camera set [parameter] [value] [options] [selectors] [general options]
```

#### Parameters:

- `audio`
  Enable or disable audio (use --enable or --disable).
- `camera-name <camera-name>`
  Set the camera name.
- `password <password>`
  Set the camera password.
- `username <username>`
  Set the camera username.
- `preview-update-rate <milliseconds>`
  Set the preview video update rate (in ms).
- `preview-quality <quality>`
  Set the preview video quality.
- `preview-resolution <resolution>`
  Set the preview video resolution.
- `preview-transmit-mode <mode>`
  Set the preview video transmit mode.
- `video-capture-mode <mode>`
  Set the video capture mode.
- `video-quality <quality>`
  Set the video quality.
- `video-resolution <resolution>`
  Set the video resolution.
- `video-transmit-mode <mode>`
  Set the video transmit mode.
- `cloud-retention <days>`
  Set the cloud retention days.
- `minimum-premise-retention <days>`
  Set the minimum premise retention days.
- `maximum-premise-retention <days>`
  Set the maximum premise retention days.
- `scene-analytics`
  Enable or disable scene analytics (use --enable or --disable).
- `cloud-preview-only`
  Enable or disable cloud-preview-only.

#### Common Options:

- `--csv`
  Display details in CSV format.
- `--file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns(use '\*' to apply to all cameras).
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by status.
- `--tag [tag1, tag2]`
  Filter by tags.

#### EXAMPLES

```bash
# Enable audio for specific cameras
een camera set audio --enable --esn 12345

# Set preview update rate and save as CSV
een camera set preview-update-rate 5000 --bridge-esn 12345 --csv -f update-rate.csv

# Set video quality
een camera set video-quality high --esn 12345

# Enable scene analytics for all cameras and export to Google Sheets
een camera set scene-analytics --enable --esn '*' -g --header
```

#### Output

When running a `camera set` command with `--csv` and `--header`, the output will be in CSV format and is suitable for scripting and automation.

**Successful Output Example:**

```text
Updated camera for 1/1 camera

"camera id","camera name","camera status","is successful"
"1002257a","93 Test Bengaluru Operations Room - PoS demo test","online","yes"
```

**Error Output Example:**

```text
Updated camera for 0/1 camera

"camera id","camera name","camera status","is successful","error reason"
"100457e6","Mobotix","online","no","Invalid argument: microphoneEnabled (response status: 400)"
```

**Scripting/AI Usage Notes:**

- The first line indicates how many cameras were updated successfully.
- The CSV output can be parsed to check the `"is successful"` column for `"yes"` or `"no"`.
- If an error occurs, the `"error reason"` column will contain the error message.
- This format is ideal for automation: scripts can check for `"yes"`/`"no"` and handle errors accordingly.

---

### delete

Delete a camera from the bridge.

#### Usage:

```
 een camera delete <esn> [general options]
```

#### Argument:

- `<esn>`
  esn of the camera to delete.

---

### add

Add camera to bridge.

#### Usage:

```
een camera add <esn> [options] [general options]
```

#### Argument:

- `<esn>`
  ESN of the bridge to which the camera will be added.

#### Required Options:

- `-C, --camera-name [camera name]`
  Specify name of the camera.
- `--guid [guid]`
  Specify GUID of the camera.

#### Options:

- `-c, --cloud-retention-days [cloud retention days]`
  Set cloud retention days for the camera.
- `-p, --password [password]`
  Set camera password.
- `-s, --scene [scene]`
  Set the camera's scene.
- `-S, --site [site]`
  Set site id of the camera.
- `-t, --tag [tag1, tag2]`
  Set camera tags.
- `-u, --username [username]`
  Set camera username.

---

### streamstatus

Get camera stream status.

#### Usage:

```
een camera streamstatus [options] [general options]
```

#### Required Options:

- `-e, --end-time [end time]`
  Specify end time of the camera stream.
- `-s, --start-time [start time]`
  Specify start time of the camera stream.

#### Optional Options:

- `--esn [esn1, esn2]`
  Filter by camera esns.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-S, --stream-type [stream type]`
  Filter by stream type for the camera.

#### Notes:

- `stream-type` can be **"fullvideo"** or **"preview"**.
- `start-time` can be **"-1h"** (one hour before current time).
- `end-time` can be **"now"** (current time).

---

### purgelist

Get camera purging and duty cycle.

#### Usage:

```
een camera purgelist [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify end time for purging.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `-l, --long`
  Display camera details including esn, bridge esn, status, resolution, cloud retention days.
- `-s, --start-time [start time]`
  Specify start time for purging.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by on site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

#### Notes:

- If you haven't specified any start-time and end-time, it will take the last 24 hours as default timestamps.

---

### i-summary

Get camera installer summary.

#### Usage:

```
een camera i-summary [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display the details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display the details in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.
- `-l, --long`
  Display details of installer summary, including duty cycle, preview size, video size, update rate (s), bandwidth speed/mode, cloud retention, minimum on premise retention, maximum on premise retention, cloud preview only (pr1), stream type.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

---

### availability

Get camera availability.

#### Usage:

```
een camera availability [options] [selectors] [general options]
```

#### Required Options:

- `-s, --start-time [start time]`
  Specify start time for video.

#### Optional Options:

- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify end time for video.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `-N, --no-check`
  Display all available data, including unchecked items.
- `-p, --preview-availability`
  Display preview recording status along with camera availability.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by on site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

#### Notes:

- This command only supports a maximum of 200 devices and a seven-day time range.

---

### addtag

The `camera addtag` command allows you to add tags to camera.
It can accept multiple tags, you can use selectors (like `--esn`, `--tag`, `--site`, etc.) to target specific cameras.

#### Usage:

```
een camera addtag <tags> [options] [selectors] [general options]
```

#### Argument:

- `<tags>`
  Tags to be added to the cameras.

#### Options:

- `--csv`
  Display details in CSV format.
- `--file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns(use '\*' to apply to all cameras)
- `--site [site name1, site name2]`
  Filter by site names.
- `--site-id [site id1, site id2]`
  Filter by site IDs.
- `--status [status]`
  Filter by status.
- `--tag [tag1, tag2]`
  Filter by tags.

#### EXAMPLES

```bash
# add tags newtag, test to camera with esn 1234
een camera addtag 'new tag, test' --esn '1234'

# add tags test to camera with bridge esn 0987 and camera status online
een camera addtag 'test' --bridge-esn '0987' --status 'online'
```

#### Output

When running a `camera addtag` command with `--csv` and `--header`, the output will be in CSV format and is suitable for scripting and automation.

**Successful Output Example:**

```csv
"camera id","camera name","camera tags","is successful","error reason"
"1234","Wiktoria regression 140525","new tag, testing","yes",""
```

**Error Output Example:**

```csv
"camera id","camera name","camera tags","is successful","error reason"
"1234","Wiktoria regression 140525","new tag, testing","no","Internal Server Error (response status: unknown)"
```

---

### deletetag

The `camera deletetag` command allows you to delete tags from selected cameras.
It can accept multiple tags, you can use selectors (like `--esn`, `--tag`, `--site`, etc.) to target specific cameras.

#### Usage:

```
een camera deletetag <tags> [options] [selectors] [general options]
```

#### Argument:

- `<tags>`
  Tags to be deleted from the cameras.

#### Options:

- `--csv`
  Display details in CSV format.
- `--file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns(use '\*' to apply to all cameras)
- `--site [site name1, site name2]`
  Filter by site names.
- `--site-id [site id1, site id2]`
  Filter by site IDs.
- `--status [status]`
  Filter by status.
- `--tag [tag1, tag2]`
  Filter by tags.

#### EXAMPLES

```bash
# delete tags newtag from camera with esns 1234,5678 give output in csv format with header:
een camera deletetag 'new tag' --esn '1234, 5678' --csv --header

# delete tags test, new tag in cameras with bridge esn 0987 and camera status online:
een camera deletetag 'test, new tag' --bridge-esn '0987' --status 'online'

```

#### Output

When running a `camera deletetag` command with `--csv` and `--header`, the output will be in CSV format and is suitable for scripting and automation.

**Successful Output Example:**

```csv
"camera id","camera name","camera tags","is successful","error reason"
"1007bdb3","Hanwha LPR Camera","lpr testing - 2.4.0","yes",""
```

**Error Output Example:**

```csv
"camera id","camera name","camera tags","is successful","error reason"
"100276a7","Wiktoria regression 140525","new tag, testing","no","Internal Server Error (response status: unknown)"
```

---

# bridge - Manage Bridges

## NAME

`bridge` - manage and interact with bridges and associated cameras.

## SYNOPSIS

```
een bridge [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `bridge` command allows you to manage bridges, list their status, check availability, pull logs, and update camera settings.

## COMMANDS

### list

List all bridges.

#### Usage:

```
een bridge list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--html`
  Generate a chart in an HTML file.
- `--include [value1, value2]`
  Display associated items (supported values: esn).
- `-l, --long`
  Display details of bridges, including bridge id, bridge name, serial number, tags, connection status, timezone, site id, site name, mac address, guid, IP address, created timestamp, number of cameras online, cloud bandwidth measured - last 7 days (mega bits per seconds), realtime bandwidth - last 7 days (mega bits per seconds), background bandwidth (background + on-demand) - last 7 days (mega bits per seconds).
- `--v1`
  Use v1 APIs.

#### Selectors:

- `-s, --status [status]`
  Filter by status.
- `--site [site name1, site name2]`
  Filter by site names.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

#### Actions:

- If `--html` is specified and `--v1`, generate a bridge list report using v1.
- If `--csv` is specified and `--v1`, list bridges in CSV format using v1.
- Handle other combinations of options to perform various listing and reporting tasks.

#### Example

To list all bridge ESNs in CSV format (with headers):

```bash
een bridge list --include 'esn' --header --csv
```

#### Output

```csv
"bridge id"
"100479d5"
"1002f572"
```

---

### availability

Get bridge availability details.

#### Usage:

```
een bridge availability [options] [selectors] [general options]
```

#### Required Options:

- `-s, --start-time [start time]`
  Specify video start time.

#### Optional Options:

- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify video end time; ensure that the --start-time option is used.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `-N, --no-check`
  Display all available data.

#### Selectors:

- `--esn [esn1, esn2]`
  Filter by bridge ESNs.
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

---

### qlstreammetrics

Pull logs from the archiver/bridge.

#### Usage:

```
een bridge qlstreammetrics [options] [general options]
```

#### Required Options:

- `--esn [esn1, esn2]`
  Specify esns of the bridge.

#### Optional Options:

- `-c, --count [count]`
  Specify the number of annotations to return.
- `-e, --end-time [end time]`
  Specify the end time.
- `-E, --events`
  Display events of the bridge.
- `-l, --local-rtsp-metrics [enable/disable]`
  Specify whether enable or disable the RTSP metrics set.
- `-p, --performance`
  Display performance metrics of the bridge.
- `-s, --start-time [start time]`
  Specify the start time.
- `-S, --summary`
  Display summarized data.

## Note:

- Along with `--esn`, one of `--events`, `--performance`, or `--local-rtsp-metrics` must be specified.

---

## EXAMPLES

- To list all bridges:

```bash
een bridge list
```

- To check the bridges with status online:

```bash
een bridge list --status 'online'  --html
```

- To get availability information for a bridge:

```bash
een bridge availability --esn [esn1, esn2] --start-time [start time] --end-time [end time]
```

---

# switch - Manage Switches

## NAME

`switch` - manage and interact with switches.

## SYNOPSIS

```
een switch [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `switch` command allows you to manage switches and list switch status.

## COMMANDS

### list

List switches.

#### Usage:

```
een switch list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. (supported values: id, name, bridge-esn, bridge, status).
- `-l, --long`
  Display details of switches including bridge id, bridge name, visibility by bridges, switch status, port count, account id.

#### Selectors:

- `--id [id1, id2]`
  Filter by switch ids.
- `--name [name]`
  Filter by switch name.

## EXAMPLES

- To list all switches:

```bash
een switch list --header --csv
```

#### Output

```csv
"switch name","switch id"
"Aut_v3_Switch_Bridge1","a7459fd0-0169-5eca-8588-17fc6c695f81"
"Switch","ac246e13-82b3-5ff7-99de-de6e4b75e64e"
```

- To list all switches with the specified ids with headers in CSV and long list format:

```bash
een switch list --id '1234, 6788' -l --header --csv
```

#### Output

```csv
"switch name","switch id","bridge id","bridge name","visible by bridges","switch status","port count","account id"
"Aut_v3_Switch_Bridge1","a7459fd0-0169-5eca-8588-17fc6c695f81","10035b4a","501 LPR Test Bengaluru Server Roomsss","406+ LPR Test Bengaluru Server room","online","8","00052029"
"Switch","ac246e13-82b3-5ff7-99de-de6e4b75e64e","-","-","DB 15 LPR Test Bridge","off","-","00052029"
```

---

# sensor - Manage Sensors

## NAME

`sensor` - manage and interact with sensors.

## SYNOPSIS

```
een sensor [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `sensor` command allows you to manage sensors and list all available sensors.

## COMMANDS

### list

List all sensors.

#### Usage:

```
een sensor list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in Google Sheets.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items (supported values: battery-level, bluetooth-signal, id, name, parent-id, status, site, site-id).
- `-l, --long`
  Display details of sensor including parent id, battery level, bluetooth signal, site id, site name, status, primary camera id, created timestamp, time zone, notes.

#### Selectors:

- `--camera-esn [esn1, esn2]`
  Filter by camera esns.
- `--id [id1, id2]`
  Filter by sensor ids.
- `--parent-id [id1, id2]`
  Filter by parent ids.
- `--site-id [site id1, site id2]`
  Filter by site ids.

## EXAMPLES

- To list all sensors with header in CSV format:

```bash
een sensor list --header --csv
```

#### Output

```csv
"id","sensor name"
"465772","BOX1 test"
"176038","BOX2"
"834978","BOX3"
```

- To list all sensors with ids 1234. 4567 with header in long list and CSV format:

```bash
een sensor list --id '834978,199109 ' --header --csv --long
```

#### Output

```csv
"id","sensor name","parent id","battery level","bluetooth signal","site id","site name","status","primary camera id","created timestamp","time zone","notes"
"834978","BOX3","347624","100","-59","0f8aedc1-af82-4950-97e5-8c154668c961","Eagle Eye Office","online","-","2025-05-21T14:10:44+00:00","US/Central","SS3-101 (A00DQA)  "
"199109","PARKING LOT 1","347624","100","-63","0f8aedc1-af82-4950-97e5-8c154668c961","Eagle Eye Office","online","-","2025-05-21T12:41:49+00:00","US/Central","SS3-101 (A00DL0)"
```

---

# speaker - Manage Speakers

## NAME

`speaker` - manage and interact with speakers.

## SYNOPSIS

```
een speaker [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `speaker` command allows you to manage speakers and list all available speakers.

## COMMANDS

### list

#### Usage:

```
een speaker list [options] [selectors] [general options]
```

List speakers.

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items (supported values: id, name).
- `-l, --long`
  Display details of speaker, including tags, site id, site name, status, GUID, account id, is shared, speaker make, visible by bridges

#### Selectors:

- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `--id [id1, id2]`
  Filter by speaker ids.
- `--name [name1, name2]`
  Filter by speaker names.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status1, status2]`
  Filter by status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

## EXAMPLES

- To list all speakers with headers in CSV format:

```bash
een speaker list --csv --header
```

#### Output

```csv
"id","name","bridge id","bridge name"
"1006cefc","Speaker AXIS C1310-E","10017196","401 AI - Parking Lot 1"
"10017fd3","Speaker EN-SDUH-001a","10017196","401 AI - Parking Lot 1"
```

- To list all speakers with bridge esn '1234', speaker id '54321,3455,2445' with headers in CSV and long list format:

```bash
een speaker list --bridge-esn '10017196' --id '1006cefc,10017fd3,100bddf1' -l --csv --header
```

#### Output

```csv
"id","name","bridge id","bridge name","tags","site name","site id","status","guid","account id","is shared","speaker make","visible by bridges"
"1006cefc","Speaker AXIS C1310-E","10017196","401 AI - Parking Lot 1","","Eagle Eye Office","0f8aedc1-af82-4950-97e5-8c154668c961","online","f4a89085-35ee-40f0-ac44-7b2fcc5ffe2c","00159662","no","axis","401 AI - Parking Lot 1 (10017196)"
"10017fd3","Speaker EN-SDUH-001a","10017196","401 AI - Parking Lot 1","parking lot 1,EN-SDUH-001a","Eagle Eye Office","0f8aedc1-af82-4950-97e5-8c154668c961","online","50436373-38ae-6f1c-0001-a2c0a4202fc4","00159662","no","eagle eye networks","401 AI - Parking Lot 1 (10017196)"
```

---

# alert - Manage Alerts

## NAME

`alert` - manage and interact with alerts.

## SYNOPSIS

```
een alert [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `alert` command allows you to manage alerts and list all alerts.

## COMMANDS

### list

List alerts.

#### Usage:

```
een alert list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. (supported values: name, id, alert-type).
- `-l, --long`
  Display alert details including id, alert type, device id, event type, event id, creator id, site id, account id, service rule id, bridge id.
- `-m, --machine-readable`
  Display details in machine-readable form.

#### Selectors:

- `--alert-name [name]`
  Filter by alert name.
- `--alert-type [type1, type2] `
  Filter by alert types. (Supported values: intrusionDetection, loitering, motionDetection, objectLineCross, personDetection, measurementThresholdStatus, tampering, vehicleDetection, deviceStatus, gunDetection, eevaQuery, lprPlateRead, motionRegionDetection, deviceIO, hotlistVehicle, watchVehicle, allowedVehicle, countOfLicensePlate, deniedVehicle, unregisteredVehicle, thermalThresholdCrossed, inputTriggered, wrongWay, slipAndFall, crowdFormation, ppeViolation, fireAndSmokeDetection).
- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `-e, --end-time [end-time]`
  Filter by end time(default: current time).
- `--esn [esn1, esn2]`
  Filter by camera ESNs.
- `--maximum-priority [number]`
  Filter by maximum priority (supported values: 0-10).
- `--minimum-priority [number]`
  Filter by minimum priority (supported values: 0-10).
- `--origin [origin]`
  Filter by origin (supported values: vsp).
- `-s, --start-time [start-time]`
  Filter by start time (default: 1 hr before now).
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site IDs.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

## EXAMPLES

- To list all alerts in CSV format with headers:

```bash
een alert list --csv --header
```

#### Output

```csv
"timestamp","alert name","device name","category","site name","priority","meta"
"2025-10-18T04:51:17.981+00:00","Motion In Region Detection Alert","CPPLUS - LPR Camera 10","video","Eagle Eye India 1","9","-"
"2025-10-18T04:51:17.756+00:00","Vehicle Detection Alert","CPPLUS - LPR Camera 9.1.1","video","Lakshmi test site 595","9","vehicleColor: gray; bodyType: car"
```

- To list all alerts for a specific alert type with headers in machine-readable form and in CSV format:

```bash
een alert list --alert--type 'personDetection' --header --csv -m
```

#### Output

```csv
"id","alert type","device id","category","event type","event id","created timestamp","creator id","site id","account id","service rule id","bridge id"
"c4c060d0-aa6b-11f0-91c9-9bd277816f28","een.personDetectionAlert.v1","1001760c","video","een.personDetectionEvent.v1","00052029-9878055a-6cb99440-fcba-4129-bd8d-de3f11606680","2025-10-16T08:40:40.695+00:00","een.events","","00052029","79480fd9-7dcb-4e1f-bee8-21289a56dd78","10035b4a"
"c4c060d0-aa6b-11f0-be8c-934bbe680362","een.personDetectionAlert.v1","1001760c","video","een.personDetectionEvent.v1","00052029-9878055a-6cb99440-fcba-4129-bd8d-de3f11606680","2025-10-16T08:40:40.697+00:00","een.events","","00052029","ecf7d429-c480-4d08-9ec3-c68906d7ce51","10035b4a"
```

- To list all alerts for camera esn '1234' with headers in long list and in CSV format:

```bash
een alert list --esn '1234' --header -l --csv
```

#### Output

```csv
"timestamp","alert name","device name","category","site name","priority","meta","id","alert type","device id","event type","event id","created timestamp","creator id","site id","account id","service rule id","bridge id"
"2025-10-18T04:53:19.218+00:00","Person Detection Alert","Wiktoria regression 140525","video","Eagle Eye India 1","9","-","5dbc0d20-abde-11f0-a3e8-f48363476040","een.personDetectionAlert.v1","100276a7","een.personDetectionEvent.v1","00052029-4ca52bb6-31653c1f-b397-48e1-bb00-1040cdc90728","2025-10-18T04:53:21.546+00:00","een.events","5acd0dd1-05a0-4d75-a14b-30e0f4083c70","00052029","79480fd9-7dcb-4e1f-bee8-21289a56dd78","10068caa"
"2025-10-18T04:53:19.218+00:00","Person Detection Alert","Wiktoria regression 140525","video","Eagle Eye India 1","10","-","5dbc0d20-abde-11f0-bf4c-67f1212ca612","een.personDetectionAlert.v1","100276a7","een.personDetectionEvent.v1","00052029-4ca52bb6-31653c1f-b397-48e1-bb00-1040cdc90728","2025-10-18T04:53:21.546+00:00","een.events","5acd0dd1-05a0-4d75-a14b-30e0f4083c70","00052029","1b8ded4e-7d71-4466-bb0e-c7146725f72d","10068caa"
```

---

# notification - Manage Notifications

## NAME

`notification` - manage and interact with notifications.

## SYNOPSIS

```
een notification [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `notification` command allows you to manage notifications and list all notifications.

## COMMANDS

### list

List notifications.

#### Usage:

```
een notification list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. Supported values: id, alert-type.
- `-l, --long`
  Display details of notifications, including id, alert type, alert id, user id, device id, validation status, account id, bridge id.
- `-m, --machine-readable`
  Display details in machine-readable form.

#### Selectors:

- `--alert-id [alert id]`
  Filter by alert id.
- `--alert-type [type1, type2] `
  Filter by alert types.(supported values: intrusionDetection, loitering, motionDetection, objectLineCross, personDetection, measurementThresholdStatus, tampering, vehicleDetection, deviceStatus, gunDetection, eevaQuery, lprPlateRead, motionRegionDetection, deviceIO, hotlistVehicle, watchVehicle, allowedVehicle, countOfLicensePlate, deniedVehicle, unregisteredVehicle, thermalThresholdCrossed, inputTriggered, wrongWay, slipAndFall, crowdFormation, ppeViolation, fireAndSmokeDetection).
- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--category [category]`
  Filter by category (values: health, video, operational, audit, job, security, sharing).
- `--max [max]`
  Filter by maximum number of notifications to display (default: 25).
- `-e, --end-time [end-time]`
  Filter by end time.
- `--esn [esn1, esn2]`
  Filter by camera ESNs.
- `--notification-status [status]`
  Filter by notification status (supported values: pending, bounced, dropped, deferred, delivered, sent, outsideUsersSchedule, notificationsDisabled, noNotificationActions, sendingFailed, throttled, unableToGetSettings).
- `-s, --start-time [start-time]`
  Filter by start time.
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.
- `--user-id [user id]`
  Filter by user id.
- `--user-name [user name]`
  Filter by user name.

## EXAMPLES

- To list all notifications details in CSV format:

```bash
een notification list --csv
```

#### Output

```csv
"2025-10-20T11:23:27.215+00:00","sent","video","LPR Camera 9","push","plateNumber: WDP7651; direction: exit; plateRegion: "
"2025-10-20T11:23:24.464+00:00","sent","video","EN-CDUB-011a-3","email","-"
```

- To list all notifications for a specific alert type with headers in machine-readable form and in CSV format:

```bash
een notification list --alert-type 'personDetection' --header --csv -m
```

#### Output

```csv
"id","alert type","alert id","category","user id","device id","validation status","account id","bridge id"
"79c23600-ada7-11f0-8ebd-e0e85d966211","een.personDetectionAlert.v1","79c23600-ada7-11f0-a3df-cb64ccbffc9a","video","ca0edebd","100954c1","","00052029","1007fda2"
"6c2f2ca0-ada7-11f0-8e48-2c6fa5757c96","een.personDetectionAlert.v1","6c2f2ca0-ada7-11f0-b351-f8eb60f88180","video","ca0edebd","100c16ad","","00052029","1007fda2"
```

- To list all notifications for category video with headers in long list and in CSV format:

```bash
een notification list --category 'video' -l --header --csv
```

#### Output

```csv
"timestamp","notification status","category","device name","notification actions","meta","id","alert type","alert id","user id","device id","validation status","account id","bridge id"
"2025-10-20T11:25:44.961+00:00","sent","video","CAMLAN Camera 1","email","-","84eacf10-ada7-11f0-b3f5-2db1a68e5554","een.personDetectionAlert.v1","84eacf10-ada7-11f0-8388-895efa10aa36","ca0edebd","10017523","","00052029","1007a214"
"2025-10-20T11:25:44.961+00:00","sent","video","CAMLAN Camera 1","email","-","84eacf10-ada7-11f0-8f64-dee519634509","een.personDetectionAlert.v1","84eacf10-ada7-11f0-a7ed-6aa9649f93ad","ca0edebd","10017523","","00052029","1007a214"
```

---

# multicamera - Manage Multicameras

## NAME

`multicamera` - Manage multicamera settings and operations

## SYNOPSIS

```
een multicamera [command] [options]
```

## COMMANDS

### list

List all multi cameras.

#### Usage:

```
een multicamera list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in csv format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items (supported values: esn, camera, bridge-esn, bridge, site, siteid, status, tag).
- `-l, --long`
  Display details of multicamera, including name, id, bridge id, bridge name, status, site name, site id, timezone, guid, tags, ip address, mac address.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.

#### Example

To list all multicameras with specific fields in CSV format (with headers):

```bash
een multicamera list --include 'esn,camera,bridge-esn,bridge,site,siteid,status,tag' --header --csv
```

#### Output

```csv
"multicamera id","multicamera name","bridge id","bridge name","site id","site name","status","tags"
"1007b4fb","Camera 47 - i-PRO WV-S8574L","10055c51","620 Enterprise Edition - Box 1","0f8aedc1-af82-4950-97e5-8c154668c961","Eagle Eye Office","bridgeOffline",""
"100c792a","Encoder EN-ECMF-001","100b7102","301 - EN-ECMF-001 - ENCODER","0f8aedc1-af82-4950-97e5-8c154668c961","Eagle Eye Office","online",""
```

---

# event - Manage Events

## NAME

`event` - manage and interact with events.

## SYNOPSIS

```
een event [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `event` command allows you to manage events and list all events.

## COMMANDS

### list

List all events.

#### Usage:

```
een event list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. Supported values: eventId,eventType.
- `-l, --long`
  Display event details including device type, id, event type, device id, event id, end time, start time, meta, creator id.
- `-m, --machine-readable`
  Display details in machine-readable form.

  ###### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `-e, --end-time [end time]`
  Filter by end time (default: current time).
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--event-type [type1,type2]`
  Filter by event types. (supported values: intrusionDetection, loitering, motionDetection, objectLineCross, personDetection, measurementThresholdStatus, tampering, vehicleDetection, deviceStatus, gunDetection, eevaQuery, lprPlateRead, deviceCreation, posTransaction, motionRegionDetection, deviceIO, hotlistVehicle, watchVehicle, allowedVehicle, countOfLicensePlate, deniedVehicle, unregisteredVehicle, thermalThresholdCrossed, inputTriggered, wrongWay, slipAndFall, crowdFormation, ppeViolation, fireAndSmokeDetection).
- `-s, --start-time [start-time]`
  Filter by start time (default: 1 hrs before now).
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

## EXAMPLES

- To list all events with headers in CSV format:

```bash
een event list --csv --header
```

```csv
"id","event type","start time","end time","meta"
"camera","2025-10-27T04:48:13.253+00:00","2025-10-27T04:48:13.253+00:00","BodyTypeConfidence: 44.9%; BodyType: car;"
"camera","2025-10-27T04:48:11.261+00:00","2025-10-27T04:48:11.261+00:00","BodyTypeConfidence: 49.8%; BodyType: car;"
```

- To list all events for a specific event type with headers in CSV format:

```bash
een event list --event-type 'vehicleDetection' --header --csv
```

#### Output

```csv
"device type","start time","end time","meta"
"camera","2025-10-27T05:45:38.618+00:00","2025-10-27T05:45:38.618+00:00","BodyTypeConfidence: 82.5%; BodyType: motorbike;"
"camera","2025-10-27T05:45:18.620+00:00","2025-10-27T05:45:18.620+00:00","BodyTypeConfidence: 44.9%; BodyType: van;"
```

- To list all events with long list in CSV format:

```bash
een event list --header --long --csv
```

#### Output

```csv
"id","event type","start time","end time","meta","device id","device type","creator id",
camera       2025-10-27T05:27:51.010+00:00  2025-10-27T05:27:51.010+00:00  -                                                00052029-032d57e9-5d58d553-21ca-4b15-88a4-24464115c517  een.personDetectionEvent.v1          100954c1   een.analytics.v1
camera       2025-10-27T05:27:51.010+00:00  2025-10-27T05:27:51.010+00:00  BodyTypeConfidence: 69.1%; BodyType: motorbike;  00052029-032d57e9-70fecbe7-c37f-42a9-aca4-4831ee531eeb  een.vehicleDetectionEvent.v1         100954c1   een.analytics.v1
```

---

# rule - Manage Rules

## NAME

`rule` - manage and interact with rules.

## SYNOPSIS

```
een rule [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `rule` command allows you to manage rule and list all rules.

## COMMANDS

### list

List all rules.

#### Usage:

```
een rule list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result. By default headers will be hidden.
- `--include [value1, value2]`
  Display associated items. Supported values: name, id, rule-type.
- `-l, --long`
  Display details of rules, including id, created timestamp, creator id, account id.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--disabled`
  Filter by disabled.
- `--enabled`
  Filter by enabled.
- `--esn [esn1, esn2]`
  Filter by camera ESNs.
- `--maximum-priority [number]`
  Filter by maximum priority (supported values: 0-10).
- `--minimum-priority [number]`
  Filter by minimum priority (supported values: 0-10).
- `--rule-type [rule type]`
  Filter by rule type (supported values: intrusionDetection, loitering, motionDetection, objectLineCross, personDetection, measurementThresholdStatus, tampering, vehicleDetection, deviceStatus, gunDetection, eevaQuery, lprPlateRead, motionRegionDetection, deviceIO, hotlistVehicle, watchVehicle, allowedVehicle, countOfLicensePlate, deniedVehicle, unregisteredVehicle, thermalThresholdCrossed, inputTriggered, wrongWay, slipAndFall, crowdFormation, ppeViolation, fireAndSmokeDetection).
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site IDs.
- `--status [status]`
  Filter by cameras status.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

## EXAMPLES

- To list all rules in CSV format with headers:

```bash
een rule list --csv --header
```

#### Output

```csv
"name","rule type","priority","devices","status","actions","insights"
"DrewTestMotion sdd","motionDetection","9","1","disable","","lastEvent: 2025-10-06T16:24:51.611+00:00; countToday: 0; countLast7Days: 0"
"Swathi_VehicleDetection_Rule001","vehicleDetection","9","6","disable","notification: Swathi_Notifications","lastEvent: -; countToday: 0; countLast7Days: 0"
```

- To list all rule for a specific rule type and enabled true with headers in CSV format:

```bash
een rule list --rule-type 'motionDetection' --enabled --header --csv
```

#### Output

```csv
"name","rule type","priority","devices","status","actions","insights"
"danny test","motionDetection","9","1","enable","notification: Danny Email","lastEvent: 2025-11-04T12:40:38.286+00:00; countToday: 2623; countLast7Days: 32805"
"wiktoria rule test 1.10.2025 no 2","motionDetection","9","3","enable","zapier: Wiktoria Zapier test","lastEvent: 2025-11-04T12:38:29.683+00:00; countToday: 434; countLast7Days: 5745"
```

- To list all rule for camera bridge esn '1234' with headers in long list and in CSV format:

```bash
een rule list --esn '1234' --header -l --csv
```

#### Output

```csv
"name","rule type","priority","devices","status","actions","insights","id","created timestamp","creator id","account id"
"DrewTestMotion sdd","motionDetection","9","1","disable","","lastEvent: 2025-10-06T16:24:51.611+00:00; countToday: 0; countLast7Days: 0","81c604fb-6d0e-4750-bf8d-5c6b65ebba0a","2024-12-10T18:10:19.978+00:00","een.events","00159662"
"Wiktoria Intrusion Zapier test","intrusionDetection","9","288","disable","zapier: Wiktoria Zapier test","lastEvent: -; countToday: 0; countLast7Days: 0","4c4c18bd-32a3-436a-ba3f-64c1f6689353","2025-05-05T09:45:28.782+00:00","een.events","00159662"
```

### delete

Delete a rule from the rule list.

#### Usage:

```
een rule delete <id> [general options]
```

#### Argument:

- `<id>`
  id of the rule to delete.

#### EXAMPLES

- To delete a rule with id '1234':

```bash
een rule delete 42d4b2f6-1aeb-4e21-84d8-1a7c46818fc4
```

#### Output

**Successful Output Example:**

```text
successfully deleted the rule: 42d4b2f6-1aeb-4e21-84d8-1a7c46818fc4
```

**Error Output Example:**

```text
error: unable to delete the rule: rule with 42d4b2f6-1aeb-4e21-84d8-1a7c46818fc4 not found (status: 404)
```

---

### add

Add a rule.

#### DESCRIPTION

The `rule add` command allows you to add a specific rule with action.
You can specify the rule type and give the options needed.

#### Usage:

```
een rule add [rule type] [options] [general options]
```

## Rule Type

### allowedvehicle

Add allowed vehicle rule.

#### Usage:

```
een rule add allowedvehicle [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.
- `--target-type [target type]`
  Specify target type (supported values: vehicleList, plate).

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--plate [plate]`
  Specify license plate number.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).
- `--vehiclelist-id [vehiclelist id]`
  Specify vehiclelist id.
- `--vehiclelist-name [vehiclelist name]`
  Specify vehiclelist name.

### countoflicenseplate

Add count of license plate rule.

#### Usage:

```
een rule add countoflicenseplate [options] [general options]
```

#### Required Options:

- `--count [count]`
  Specify count.
- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--duration [duration]`
  Specify duration in minutes (default to 5 minutes).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--rule-value [value]`
  Specify rule value (supported values: greaterThan, lessThan).
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### crowdformation

Add crowd formation rule.

#### Usage:

```
een rule add crowdformation [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### deniedvehicle

Add denied vehicle rule.

#### Usage:

```
een rule add deniedvehicle [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.
- `--target-type [target type]`
  Specify target type (supported values: vehicleList, plate).

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--plate [plate]`
  Specify license plate number.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).
- `--vehiclelist-id [vehiclelist id]`
  Specify vehiclelist id.
- `--vehiclelist-name [vehiclelist name]`
  Specify vehiclelist name.

### devicestatus

Add device status rule.

#### Usage:

```
een rule add devicestatus [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--device-type [type]`
  Specify device type (supported values: camera, speaker).
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--device-id [id1, id2]`
  Specify device ids.
- `--device-name [name1, name2]`
  Specify device names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### eevaevent

Add eeva event rule.

#### Usage:

```
een rule add eevaevent [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### fireandsmokedetection

Add fire and smoke detection rule.

#### Usage:

```
een rule add fireandsmokedetection [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### gundetection

Add gun detection rule.

#### Usage:

```
een rule add gundetection [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### hotlistvehicle

Add hotlist vehicle rule.

#### Usage:

```
een rule add hotlistvehicle [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.
- `--target-type [target type]`
  Specify target type (supported values: vehicleList, plate).

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--plate [plate]`
  Specify license plate number.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).
- `--vehiclelist-id [vehiclelist id]`
  Specify vehiclelist id.
- `--vehiclelist-name [vehiclelist name]`
  Specify vehiclelist name.

### inputtriggered

Add input triggered rule.

#### Usage:

```
een rule add inputtriggered [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--device-type [type]`
  Specify device type (supported values: camera, speaker).
- `--input-port [port]`
  Specify input port.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--device-id [id1, id2]`
  Specify device ids.
- `--device-name [name1, name2]`
  Specify device names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### intrusiondetection

Add intrusion detection rule.

#### Usage:

```
een rule add intrusiondetection [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### loitering

Add loitering rule.

#### Usage:

```
een rule add loitering [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### measurementthresholdstatus

Add measurement threshold status rule.

#### Usage:

```
een rule add measurementthresholdstatus [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--measurement-id [id1, id2]`
  Specify measurement ids.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### motiondetection

Add motion detection rule.

#### Usage:

```
een rule add motiondetection [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### motionregiondetection

Add motion region detection rule.

#### Usage:

```
een rule add motionregiondetection [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### objectlinecross

Add object line cross rule.

#### Usage:

```
een rule add objectlinecross [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### persondetection

Add person detection rule.

#### Usage:

```
een rule add persondetection [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### ppeviolation

Add ppe violation rule.

#### Usage:

```
een rule add ppeviolation [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### slipandfall

Add slip and fall rule.

#### Usage:

```
een rule add slipandfall [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### thermalthresholdcrossed

Add thermal threshold crossed rule.

#### Usage:

```
een rule add thermalthresholdcrossed [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### unregisteredvehicle

Add unregistered vehicle rule.

#### Usage:

```
een rule add unregisteredvehicle [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).
- `--vehiclelist-id [vehiclelist id]`
  Specify vehiclelist id.
- `--vehiclelist-name [vehiclelist name]`
  Specify vehiclelist name.

### vehicledetection

Add vehicle detection rule.

#### Usage:

```
een rule add vehicledetection [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

### watchvehicle

Add watch vehicle rule.

#### Usage:

```
een rule add watchvehicle [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.
- `--target-type [target type]`
  Specify target type (supported values: vehicleList, plate, anyPlateExcept).

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--destination-camera [camera1, camera2]`
  Specify destination camera names.
- `--destination-esn [esn1, esn2]`
  Specify destination camera esns.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--duration [duration]`
  Specify duration in minutes (default to 5 minutes).
- `--exemption-vehiclelist-id [exemption vehiclelist id]`
  Specify exemption vehiclelist id.
- `--exemption-vehiclelist-name [exemption vehiclelist name]`
  Specify exemption vehiclelist name.
- `--notes [notes]`
  Specify notes.
- `--origin-camera [camera1, camera2]`
  Specify origin camera names.
- `--origin-esn [esn1, esn2]`
  Specify origin camera esns.
- `--plate [plate]`
  Specify license plate number.
- `--vehiclelist-id [vehiclelist id]`
  Specify vehiclelist id.
- `--vehiclelist-name [vehiclelist name]`
  Specify vehiclelist name.

### wrongway

Add wrong way rule.

#### Usage:

```
een rule add wrongway [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify rule name.
- `--priority [priority]`
  Specify priority.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids.
- `--action-name [name1, name2]`
  Specify action names.
- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the rule status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (defaults to 24 hours).

#### EXAMPLES

- To add rule for eevaevent with name 'name', priority 5, schedule work hours, for specified cameras with specified actions:

```bash
een rule add eevaevent --name 'evaa rule' --priority '5' --schedule 'workHours' --camera 'FFserver-Test testing  ' --esn '10037500' --action-name 'R2' --action-id 'e9a6a541-6cdf-4f3c-a0e4-410478f51595'
```

#### Output

**Successful Output Example:**

```text
successfully added rule with action: (id: f169315d-a76c-4f2f-9924-5958cc74e44b)
```

**Error Output Example:**

```text
unable to add rule: same rule already exists (status: 409)
```

---

### set

Update rule.

#### DESCRIPTION

The `rule set` command allows you to update the rule for the specified id.
You can specify the id of rule to change as `<parameter>` and specify options to change.

#### Usage:

```
een rule set <id> [options] [general options]
```

#### Arguments:

- `<id>`
  Id of the rule to update.

#### Options:

- `--action-id [id1, id2]`
  Specify action ids (supported by: all types).
- `--action-name [name1, name2]`
  Specify action names (supported by: all types).
- `--camera [camera1, camera2]`
  Specify camera names (supported by: intrusionDetection, loitering, motionDetection, motionRegionDetection, objectLineCross, thermalThresholdCrossed, vehicleDetection, personDetection, eevaQuery, gunDetection, slipAndFall, crowdFormation, ppeViolation, fireAndSmokeDetection, allowedVehicle, deniedVehicle, countOfLicensePlate, unregisteredVehicle, hotlistVehicle, wrongWay).
- `--count [count]`
  Specify count (supported by: countOfLicensePlate).
- `--destination-camera [camera1, camera2]`
  Specify destination camera names (supported by: watchVehicle).
- `--destination-esn [esn1, esn2]`
  Specify destination camera esns (supported by: watchVehicle).
- `--device-id [id1, id2]`
  Specify device ids (supported by: inputTriggered, deviceStatus).
- `--device-name [name1, name2]`
  Specify device names (supported by: inputTriggered, deviceStatus).
- `--device-type [type]`
  Specify device type (supported values: camera, speaker) (supported by: inputTriggered, deviceStatus).
- `--disable`
  Set the rule status to disabled (supported by: all types).
- `--duration [duration]`
  Specify duration in minutes (supported by: watchVehicle, countOfLicensePlate).
- `--enable`
  Set the rule status to enabled (supported by: all types).
- `--esn [esn1, esn2]`
  Specify camera esns (supported by: intrusionDetection, loitering, motionDetection, motionRegionDetection, objectLineCross, thermalThresholdCrossed, vehicleDetection, personDetection, eevaQuery, gunDetection, slipAndFall, crowdFormation, ppeViolation, fireAndSmokeDetection, allowedVehicle, deniedVehicle, countOfLicensePlate, unregisteredVehicle, hotlistVehicle, wrongWay).
- `--exemption-vehiclelist-id [exemption vehiclelist id]`
  Specify exemption vehiclelist id (supported by: watchVehicle).
- `--exemption-vehiclelist-name [exemption vehiclelist name]`
  Specify exemption vehiclelist name (supported by: watchVehicle).
- `--input-port [port1, port2]`
  Specify input ports (supported by: inputTriggered).
- `--measurement-id [id1, id2]`
  Specify measurement ids (supported by: measurementThresholdStatus).
- `--name [name]`
  Specify rule name (supported by: all types).
- `--notes [notes]`
  Specify notes (supported by: all types).
- `--origin-camera [camera1, camera2]`
  Specify origin camera names (supported by: watchVehicle).
- `--origin-esn [esn1, esn2]`
  Specify origin camera esns (supported by: watchVehicle).
- `--plate [plate]`
  Specify license plate number (supported by: allowedVehicle, deniedVehicle, hotlistVehicle, watchVehicle).
- `--priority [priority]`
  Specify priority (supported by: all types).
- `--rule-type [rule type]`
  Specify rule type (supported values: intrusionDetection, loitering, motionDetection, motionRegionDetection, objectLineCross, personDetection, measurementThresholdStatus, tampering, gunDetection, vehicleDetection, deviceStatus, eevaQuery, hotlistVehicle, watchVehicle, allowedVehicle, countOfLicensePlate, deniedVehicle, unregisteredVehicle, thermalThresholdCrossed, deviceIO, inputTriggered, wrongWay, slipAndFall, crowdFormation, ppeViolation, fireAndSmokeDetection) (supported by: all types).
- `--rule-value [value]`
  Specify rule value (supported values: greaterThan, lessThan) (supported by: countOfLicensePlate).
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours) (supported by: intrusionDetection, loitering, motionDetection, motionRegionDetection, objectLineCross, thermalThresholdCrossed, vehicleDetection, personDetection, eevaQuery, gunDetection, slipAndFall, crowdFormation, ppeViolation, fireAndSmokeDetection, allowedVehicle, deniedVehicle, countOfLicensePlate, unregisteredVehicle, hotlistVehicle, wrongWay, measurementThresholdStatus, inputTriggered, deviceStatus, deviceIO).
- `--target-type [target type]`
  Specify target type (supported values: vehicleList, plate, anyPlateExcept) (supported by: allowedVehicle, deniedVehicle, hotlistVehicle, watchVehicle).
- `--vehiclelist-id [vehiclelist id]`
  Specify vehiclelist id (supported by: allowedVehicle, deniedVehicle, hotlistVehicle, watchVehicle, unregisteredVehicle).
- `--vehiclelist-name [vehiclelist name]`
  Specify vehiclelist name (supported by: allowedVehicle, deniedVehicle, hotlistVehicle, watchVehicle, unregisteredVehicle).

#### EXAMPLES

- To update rule with id '1234' to set the name as 'name' and disable the rule:

```bash
een rule set 4879606b-1b89-4c74-8080-25cbf93faffc --name 'new unregistered test' --disable
```

#### Output

**Successful Output Example:**

```text
successfully updated the rule: (id: 4879606b-1b89-4c74-8080-25cbf93faffc)
```

**Error Output Example:**

```text
unable to update rule: rule with 4879606b-1b89-4c74-8080-25cbf93faffc not found (status: 404)
```

---

# action - Manage Action

## NAME

`action` - manage and interact with actions.

## SYNOPSIS

```
een action [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `action` command allows you to manage action and list all actions.

## COMMANDS

### list

List all actions.

#### Usage:

```
een action list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  List details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in CSV format in google sheet.
- `--header`
  Display column headers in the result. By default headers will be hidden.
- `--include [value1, value2]`
  Display associated items. (supported values: id, name, action-type, recipients-name).
- `-l, --long`
  Display action details including id, created timestamp, rearm seconds, max per hour, site url, email, port, user name, password, tls, duration, port id, device id.

#### Selectors:

- `--action-type [type]`
  Filter by action types (supported values: immix, sentinal, notification, webhook, zapier, outputPort, smsMmsNotification, ebus).

## EXAMPLES

- To list all action in CSV format with headers:

```bash
een action list --csv --header
```

#### Output

```csv
"name","action type","recipients","status"
"Yen Test","notification","1","disable"
"Alert Shubham & Hari","notification","2","enable"
"Alert Hari","notification","1","enable"
```

- To list all action for a specific action type with headers in long list format:

```bash
een action list --action-type 'zapier' --header --csv
```

#### Output

```csv
"name","action type","recipients","status","id","created timestamp","rearm seconds","max per hour"
"000 wiktoria action test","zapier","","disable","d1349bc4-96d0-4c6f-930f-edc870e2abbc","2024-12-18T11:08:26.887+00:00","",""
"Zapier wiktoria test","zapier","","disable","8371abcd-313d-4ee2-96ee-0c78da658a36","2025-02-12T14:13:47.300+00:00","",""
```

---

### add

Add actions.

#### DESCRIPTION

The `action add` command allows you to add a specific action.
You can specify the action type to add as `<parameter>`, and give the options.

#### Usage:

```
een action add [action type] [options] [general options]
```

## Action Type

### ebus

Add ebus action.

#### Usage:

```
een action add ebus [options] [general options]
```

#### Required Options:

- `--email [email]`
  Specify email address.
- `--name [name] `
  Specify action name.
- `--port [port]`
  Specify port id.
- `--url [url]`
  Specify url or ip address .

#### Options:

- `--disable`
  Set the action status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.
- `--password [password]`
  Specify password.
- `--username [username]`
  Specify user name.

#### EXAMPLES

- To add action for ebus with name 'ebus test', email 'test@gmail.com', port 45 and url '112.111.2.1':

```bash
een action add ebus --name 'ebus cli' --email 'test@gmail.com' --port '45' --url '112.111.2.1'
```

#### Output

**Successful Output Example:**

```text
ebus action added successfully (id: b2c25698-0d7d-4d37-b406-0c7b30e6dfef)
```

**Error Output Example:**

```text
failed to add action — Invalid argument: port (status: 400)
```

### immix

Add immix action.

#### Usage:

```
een action add immix [options] [general options]
```

#### Required Options:

- `--email [email]`
  Specify email address.
- `--name [name] `
  Specify action name.
- `--port [port]`
  Specify port id.
- `--url [url]`
  Specify url or ip address .

#### Options:

- `--bounding-box`
  Specify whether to enable bounding box.
- `--disable`
  Set the action status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.
- `--password [password]`
  Specify password.
- `--tls`
  Specify whether to enable tls.
- `--username [username]`
  Specify user name.

#### EXAMPLES

- To add action for immix with name 'immix test', email 'test@gmail.com', port 45, url 'https://.../' and username 'testuser' :

```bash
een action add immix --name 'immix cli' --email 'test@gmail.com' --port '45' --url 'https://.***com/' --username 'testuser'
```

#### Output

**Successful Output Example:**

```text
immix action added successfully (id: b2c25698-0d7d-4d37-b406-0c7b30e6dfef)
```

**Error Output Example:**

```text
failed to add action — Invalid argument: port (status: 400)
```

### notification

Add notification action.

#### Usage:

```
een action add notification [options] [general options]
```

#### Required Options:

- `--name [name] `
  Specify action name.
- `--notification-type [type1, type2]`
  Specify notification types (supported values: email, push).

#### Options:

- `--disable`
  Set the action status to disabled (enabled by default).
- `--max-per-hour [max per hour]`
  Specify max per hour.
- `--notes [notes]`
  Specify notes.
- `--rearm [rearm]`
  Specify rearm in seconds.
- `--user-id [id1, id2]`
  Specify user ids.
- `--user-name [name1, name2]`
  Specify user names.

#### EXAMPLES

- To add action for notification with name 'notification test', notification type 'email,push', user id '1234':

```bash
een action add notification --name 'notification cli' --notification-type 'email,push' --user-id 'ca08f'
```

#### Output

**Successful Output Example:**

```text
notification action added successfully (id: ae834f23-f70a-4adf-8f1f-6dc8dabec42f)
```

**Error Output Example:**

```text
failed to add action — users.0.id: ID must be 8 lowercase letters or digits. (status: 400)
```

### outputport

Add outputport action.

#### Usage:

```
een action add outputport [options] [general options]
```

#### Required Options:

- `--device-id [device id]`
  Specify device id.
- `--duration [duration]`
  Specify duration in seconds.
- `--name [name] `
  Specify action name.
- `--port [port]`
  Specify port id.

#### Options:

- `--disable`
  Set the action status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.

#### EXAMPLES

- To add action for outputport with name 'outputport test', device id '1234', port 'relay_1', duration 20:

```bash
een action add outputport --device-id '1009f415' --port 'relay_1' --duration '20' --name 'outputport cli'
```

#### Output

**Successful Output Example:**

```text
outputPort action added successfully (id: 233e8083-b6a8-44b9-bd37-1ac2425d227c)
```

**Error Output Example:**

```text
failed to add action — Invalid argument: portId (status: 400)
```

### sentinel

Add monitor computer system-sentinel action.

#### Usage:

```
een action add sentinel [options] [general options]
```

#### Required Options:

- `--name [name] `
  Specify action name.
- `--url [url]`
  Specify url.

#### Options:

- `--disable`
  Set the action status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.

#### EXAMPLES

- To add action for sentinel with name 'sentinel test', url 'https://\*\*\*.com/':

```bash
een action add sentinel --url 'https://***.com/' --name 'sentinel test'
```

#### Output

**Successful Output Example:**

```
sentinel action added successfully (id: 0263e5d6-d76a-4613-931e-4e8f8fa9f6bd)
```

**Error Output Example:**

```text
failed to add action — Invalid argument: url (status: 400)
```

### smsmms

Add SMS/MMS notification action.

#### Usage:

```
een action add smsmms [options] [general options]
```

#### Required Options:

- `--name [name] `
  Specify action name.

#### Options:

- `--disable`
  Set the action status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.
- `--user-id [id1, id2]`
  Specify user ids.
- `--user-name [name1, name2]`
  Specify user names.

#### EXAMPLES

- To add action for smsmms with name 'smsmms test', user id '1234':

```bash
een action add smsmms --name 'smsmmstest' --user-id 'ca08135f'
```

#### Output

**Successful Output Example:**

```
sms action added successfully (id: fcdd212e-d378-4ecf-8714-dc1788c7a9b6)
```

**Error Output Example:**

```text
failed to add action — users.0.id: ID must be 8 lowercase letters or digits. (status: 400)
```

### webhook

Add webhook action.

#### Usage:

```
een action add webhook [options] [general options]
```

#### Required Options:

- `--name [name] `
  Specify action name.
- `--url [url]`
  Specify url.

#### Options:

- `--disable`
  Set the action status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.

#### EXAMPLES

- To add action for webhook with name 'webhook test', url 'https://\*\*\*.com/':

```bash
een action add webhook --url 'https://***.com/' --name 'webhook test'
```

#### Output

**Successful Output Example:**

```
webhook action added successfully (id: 9269483b-9300-4e45-a2ab-0c087e93c09e)
```

**Error Output Example:**

```text
failed to add action — Invalid argument: url (status: 400)
```

### zapier

Add zapier action.

#### Usage:

```
een action add zapier [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify action name.
- `--url [url]`
  Specify url.

#### Options:

- `--disable`
  Set the action status to disabled (enabled by default).
- `--notes [notes]`
  Specify notes.

#### EXAMPLES

- To add action for zapier with name 'name' and url 'https://.../':

```bash
een action add zapier --name 'zapier cli' --url 'https://mail.******.com/'
```

#### Output

**Successful Output Example:**

```text
zapier action added successfully (id: 9f0121aa-1241-46d4-884b-110ca780f3e7)
```

**Error Output Example:**

```text
failed to add action — Invalid argument: url (status: 400)
```

---

### delete

Delete an action from the action list.

#### Usage:

```
een action delete <id> [general options]
```

#### Argument:

- `<id>`
  id of the action to delete.

#### EXAMPLES

- To delete an action with id '1234':

```bash
een action delete 'ed4e7090-23ee-41dc-bf5a-58df32cdd960'
```

#### Output

**Successful Output Example:**

```text
successfully deleted the action: ed4e7090-23ee-41dc-bf5a-58df32cdd960
```

**Error Output Example:**

```text
error: unable to delete the action: ed4e7090-23ee-41dc-bf5a-58df32cdd960
```

---

### set

Update action.

#### DESCRIPTION

The `action set` command allows you to update the action for the specified id.
You can specify the id of action to change as `<parameter>` and specify options to change.

#### Usage:

```
een action set <id> [options] [general options]
```

#### Arguments:

- `<id>`
  Id of the action to update.

#### Options:

- `--bounding-box [boolean]`
  Specify whether to enable or disable bounding box (supported by: immix).
- `--device-id [device id]`
  Specify device id (supported by: outputPort).
- `--disable`
  Set the action status to disabled (supported by: all types).
- `--duration [duration]`
  Specify duration in seconds (supported by: outputPort).
- `--email [email]`
  Specify email address (supported by: immix, ebus).
- `--enable`
  Set the rule status to enabled (supported by: all types).
- `--max-per-hour [max per hour]`
  Specify max per hour (supported by: notification).
- `--name [name]`
  Specify action name (supported by: all types).
- `--notes [notes]`
  Specify notes (supported by: all types).
- `--notification-type [type1, type2]`
  Specify notification types (supported values: email, push) (supported by: notification).
- `--password [password]`
  Specify password (supported by: immix, ebus).
- `--port [port]`
  Specify port id (supported by: immix, outputPort, ebus).
- `--rearm [rearm]`
  Specify rearm in seconds (supported by: notification).
- `--tls [boolean]`
  Specify whether to enable or disable tls (supported by: immix).
- `--url [url]`
  Specify url (supported by: immix, sentinel, webhook, zapier, ebus).
- `--user-id [user id1, user id2]`
  Specify user ids (supported by: notification, sms).
- `--user-name [name1, name2]`
  Specify user names (supported by: immix, notification, sms, ebus).

#### EXAMPLES

- To update action for zapier with id '1234' set name 'name' and disable the action:

```bash
een action set 76e44752-cc39-4e9f-b65c-9313b961a896 --notes 'zapier action' --name 'zapier update' --disable
```

#### Output

**Successful Output Example:**

```text
successfully updated action: (id: 76e44752-cc39-4e9f-b65c-9313b961a896)
```

**Error Output Example:**

```text
unable to update action: the resource was not found (status: 404)
```

---

# role - Manage Roles

## NAME

`role` - manage and interact with roles.

## SYNOPSIS

```
een role [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `role` command allows you to manage roles in current user's account, including listing all available roles.

## COMMANDS

### list

List of all roles in current user's account.

#### Usage

```
een role list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items (supported values: role-id, role-name, users, default-role).
- `-l, --long`
  Display details of role including role id, is assignable and permissions.

#### Selectors:

- `--role [role name]`
  Filter by role name.
- `--role-id [id1, id2]`
  Filter by role IDs.

## EXAMPLES

- To list all roles with headers in CSV format:

```bash
een role list --header --csv
```

#### Output

```csv
"role name","description","users","default role"
"Administrator","Default administrator role","3","false"
"Test role 724","Test role 724","1","false"
```

- To get role with role name 'Viewers' in CSV format with headers:

```bash
een role list --role 'Viewers' --header --csv
```

#### Output

```csv
"role name","description","users","default role"
"Administrator","Default administrator role","3","false"
```

- To get roles with id '1234,4321' in long list and CSV format with headers:

```bash
een role list --role-id '8b284309-062a-4d50-af1c-fff4de07f122, 7e7b9e69-5112-4bb2-ba4e-08c061f8dbd5' --header --csv --long
```

#### Output

```csv
"role name","description","users","default role","role id","is assignable","permissions"
"Viewers","Default viewer role","3","false","8b284309-062a-4d50-af1c-fff4de07f122","true","viewLiveVideo,viewHistoricVideo,downloadVideo,viewPreviewVideo"
"Administrator","Default administrator role","3","false","8b284309-062a-4d50-af1c-fff4de07f122","true","viewLiveVideo,viewHistoricVideo,downloadVideo,viewPreviewVideo"
```

---

# site - Manage Sites

## NAME

`site` - manage and interact with sites.

## SYNOPSIS

```
een site [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `site` command allows you to manage sites, including listing all available sites.

## COMMANDS

### list

List all sites.

#### Usage

```
een site list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items (supported values: site-id, site-name).
- `-l, --long`
  Display details of site including address, city, region, postal code, country, camera count, bridge count, user count, speaker count, multi camera count.

#### Selectors:

- `--city [city1, city2]`
  Filter by city.
- `--country [country1, country2]`
  Filter by country.
- `--postal-code [postal code1, postal code2]`
  Filter by postal code.
- `--region [region1, region2]`
  Filter by region.
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.

## EXAMPLES

- To list all sites in CSV format:

```bash
een site list --csv --header
```

#### Output

```csv
"site name","site id"
"Eagle Eye Bangalor","83860e96-cd90-4b32-ba41-5866e3088927"
"Eagle Eye India 1","5acd0dd1-05a0-4d75-a14b-30e0f4083c70"
```

- To get sites list with site name 'eagle eye', city 'bangalore' in CSV and long list format with header:

```bash
een site list --site 'Eagle Eye Bangalor' --city 'Bangalore' --header -l --csv
```

#### Output

```csv
"site name","site id","address","city","region","postal code","country","camera count","bridge count","user count","speaker count","multi camera count"
"Eagle Eye Bangalor","83860e96-cd90-4b32-ba41-5866e3088927","Sri Krishna Temple Road, Indira Nagar,","Bangalore","Karanataka","560038","India","3","1","-","-","-"
```

- To get sites list with site id '1234', region 'Karnataka' in CSV and long list format with header:

```bash
een site list --site-id '5acd0dd1-05a0-4d75-a14b-30e0f4083c70' --region 'Karnataka' -l --header --csv
```

#### Output

```csv
"site name","site id","address","city","region","postal code","country","camera count","bridge count","user count","speaker count","multi camera count"
"Eagle Eye India 1","5acd0dd1-05a0-4d75-a14b-30e0f4083c70","Ginserv, Leela Palace Road,, Kodihalli, ","Bangalore","Karnataka","560008","India","21","3","1","-","-"
```

---

# download - Manage Downloads

## NAME

`download` - manage and interact with downloads, including videos and previews.

## SYNOPSIS

```
een download [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `download` command allows you to export, list, get and delete video downloads, and get previews.

#### Usage:

```
een download [command] [options]
```

## COMMANDS

### video

Manage video downloads.

#### Usage:

```
een download video [command] [options]
```

#### Subcommands:

##### list

List all videos.

#### Usage:

```
een download video list [options] [selectors] [general options]
```

###### Options:

- `--csv`
  Display details in CSV format.
- `--file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. Supported values: id, name, dfilename.
- `-l, --long`
  Display details of videos, including id, name, dfilename, camera id, start time, end time, timezone.

###### Selectors:

- `-C, --camera [camera]`
  Filter by camera name.
- `--esn [esn]`
  Filter by camera esn.

---

##### video export

Export video.

#### Usage:

```
een download video export [options] [general options]
```

#### Required Options:

- `-s, --start-time [start time]`
  Specify start time.

###### Options:

- `-C, --camera [camera]`
  Specify camera name.
- `-e, --end-time [end time]`
  Specify end time.
- `--esn [esn]`
  Specify camera ESN.
- `--length [length]`
  Specify length from start time in seconds.
- `--max-length [max length] `
  Specify maximum duration in seconds for time-lapse video.
- `--name [name]`
  Specify export file name.
- `-T, --timezone [timezone]`
  Specify timezone for timestamp (default: camera's timezone).
- `--time-lapse`
  Export a time-lapsed video.
- `--timestamp`
  Specify timestamp.

---

##### video get

Download video.

#### Usage:

```
een download video get [options] [general options]
```

###### Options:

- `--dfilename [dfilename]`
  Specify file name to download.
- `--directory [directory]`
  Specify output directory.
- `-f, --file-name [file-name]`
  Specify override output file name.
- `--id [id]`
  Specify id of video to be downloaded.
- `--name [name]`
  Specify name of video to be downloaded.

---

##### video delete

Delete a video by ID.

#### Usage:

```
een download video delete <video-id> [general options]
```

###### Arguments:

- `<video-id>`
  The ID of the video to delete.

---

### preview

Download preview.

#### Usage:

```
een download preview [options] [selectors] [general options]
```

#### Required Options:

- `-s, --start-time [start time]`
  Specify start time.

#### Options:

- `--directory [directory]`
  Specify output directory.
- `-e, --end-time [end time]`
  Specify end time.
- `--length [length]`
  Specify length from start time in seconds.
- `--overlay`
  Specify overlay.
- `-T, --timezone [timezone]`
  Specify timezone for timestamp (default: camera's timezone).

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--site [site name1, site name2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

## EXAMPLES

- To list all videos available for download:

```bash
een download video list
```

- To list videos with specific details in CSV format:

```bash
een download video list --include 'id,name,dfilename' --csv --header
```

- To export a video with timestamp:

```bash
een download video export --esn 12345 --start-time "20241001000000.000" --end-time "20241001010000.000" --timestamp
```

- To download a specific video by ID:

```bash
een download video get --id "12345" --directory "/path/to/save"
```

- To download a preview from a camera:

```bash
een download preview --esn 12345 --start-time "20241001000000.000" --end-time "20241001010004.000" --directory "/path/to/save"
```

- To download preview from cameras with specified bridge esn and camera status online:

```bash
een download preview --bridge-esn 12345 --status 'online' --start-time "20241001000000.000" --length 3
```

- To delete a video by ID:

```bash
een download video delete video123
```

---

# job - Manage Jobs

## NAME

`job` - manage and interact with jobs.

## SYNOPSIS

```
een job [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `job` command allows you to list and manage jobs in the system.

## COMMANDS

### list

List jobs.

#### Usage:

```
een job list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `--jobid [id]`
  Filter by job ID.
- `--jobstate [state]`
  Filter by job state (supported values: pending, started, failure, success, revoked).

## EXAMPLES

- To list all jobs:

```bash
een job list --csv
```

#### Output

```csv
"dfe14ab2-b33d-4a6e-ab73-c4a446c8f1ac","reports.vsp-events","failure","0%"
"20146d9d-1752-447c-b35f-1b76d5f25a4f","reports.vsp-events","failure","0%"
```

- To list jobs with headers in CSV format:

```bash
een job list --csv --header
```

#### Output

```csv
"id","type","state","progress"
"dfe14ab2-b33d-4a6e-ab73-c4a446c8f1ac","reports.vsp-events","failure","0%"
"20146d9d-1752-447c-b35f-1b76d5f25a4f","reports.vsp-events","failure","0%"
```

- To list jobs with a specific state:

```bash
een job list --jobstate success --header --csv
```

#### Output

```csv
"id","type","state","progress"
"8126210f-ed1e-471e-b8b6-6ccf2c58a3fe","reports.audit-log","success","100%"
"2493b136-96a1-45b0-b553-789503981702","reports.audit-log","success","100%"
```

- To list pending jobs and save to file:

```bash
een job list --jobstate pending --csv --file-name pending_jobs.csv
```

- To list a specific job by ID:

```bash
een job list --jobid "123456"
```

---

# video - Manage Recorded Videos

## NAME

`video` - manage and interact with recorded videos.

## SYNOPSIS

```
een video [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `video` command allows you to check the status of preview recordings.

#### Usage:

```
een video [command] [options]
```

## COMMANDS

### previewrecordingstatus

Get the status of preview recording.

#### Usage:

```
een video previewrecordingstatus [options] [general options]
```

#### Required Options:

- `--esn [esn1, esn2]`
  Specify esns of the camera.
- `-s, --start-time [start time]`
  Specify video start time.

#### Optional Options:

- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify video end time.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Actions:

- If ESNs and start time are provided, it checks the preview recording status. If the `--google-sheet` option is provided, the statuses will be listed in Google Sheets.

## EXAMPLES

- To check the status of a preview recording:

```bash
een video previewrecordingstatus --esn 1005f355 --start-time  2024-11-17T09:20:54.619+00:00 --end-time  2024-11-18T09:20:54.619+00:00 --debug
```

---

# vsp - Manage Vehicle Surveillance Package (VSP) Events and Alerts

## NAME

`vsp` - manage and retrieve Vehicle Surveillance Processing events and alerts.

## SYNOPSIS

```
een vsp [command] [options]
```

## DESCRIPTION

The `vsp` command allows you to manage and retrieve VSP events, alerts, vehiclelist and vehicle details based on parameters such as time, vehicle characteristics, and alert types.

## COMMANDS

### list

#### Usage:

```
een vsp list [command] [options]
```

## DESCRIPTION

Manage and list various VSP-related entities.

## COMMANDS

### events

List VSP events.

#### Usage:

```
een vsp list events [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify LPR end time; ensure that the --start-time option is used.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--html`
  Generate chart in HTML file.
- `-s, --start-time [start time]`
  Specify LPR start time.

#### Selectors:

- `-a, --access-type [access types]`
  Filter by access types.
- `-b, --body-type [types]`
  Filter by vehicle body types.
- `-c, --color [colors]`
  Filter by vehicle colors.
- `-D, --direction [directions]`
  Filter by direction of the vehicle.
- `--esn [esn1, esn2]`
  Filter by camera ESNs.
- `--lp [lp]`
  Filter by license plate number.
- `-m, --make [makes]`
  Filter by vehicle makes.
- `--site [site name1, site name2]`
  Filter by site name. Provide a comma-separated list of site names.
- `--site-id [site id1, site id2]`
  Filter by site id. Provide a comma-separated list of site IDs.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.

#### Actions:

- If `--html` is specified, it generates a report of VSP events.
- If not, it retrieves VSP events and saves them according to the specified options.

---

### alerts

List VSP alerts.

#### Usage:

```
een vsp list alerts [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify LPR end time; ensure that the --start-time option is used.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--html`
  Generate chart in HTML file.
- `-s, --start-time [start time]`
  Specify LPR start time.

#### Selectors:

- `-a, --allowed-vehicle`
  Filter by alert type - allowed vehicle.
- `-c, --count-of-license-plate`
  Filter by alert type - count of license plate.
- `-D, --denied-vehicle`
  Filter by alert type - denied vehicle.
- `--esn [esn1, esn2]`
  Filter by camera ESNs.
- `-H, --hotlist`
  Filter by alert type - hotlist.
- `--site [site name1, site name2]`
  Filter by alerts in the specified sites. Provide a comma-separated list of site names.
- `--site-id [site id1, site id2]`
  Filter by alerts in the specified sites. Provide a comma-separated list of site IDs.
- `-u, --unregistered-vehicle`
  Filter by alert type - unregistered vehicle.
- `-w, --watch-vehicle`
  Filter by alert type - watch vehicle.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.

#### Actions:

- If `--html` is specified, it generates a report of VSP alerts.
- If not, it retrieves VSP alerts and saves them according to the specified options.

## EXAMPLES

- To get VSP events for a specific time frame:

```bash
een vsp list events --start-time "20241001000000.000" --end-time "20241001235959.000"
```

- To get VSP alerts for allowed vehicles:

```bash
een vsp list alerts --start-time 2024-11-17T09:20:54.619+00:00 --end-time 2024-11-18T09:20:54.619+00:00 --allowed-vehicle
```

---

# vehiclelist - Manage Vehiclelist

## NAME

`vehiclelist` - manage and interact with vehiclelist.

## SYNOPSIS

```
een vehiclelist [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `vehiclelist` command allows you to manage vehiclelist and list all vehiclelist.

## COMMANDS

### add

Add vehiclelist.

#### Usage:

```
een vehiclelist add [options] [general options]
```

#### Required Options:

- `--name [name]`
  Specify vehiclelist name.

#### Options:

- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the vehiclelist status to disabled (enabled by default).
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--notes [notes]`
  Specify notes.

#### EXAMPLES

- To add a vehiclelist with name 'name' and cameras '108 Test camera (RMA ROOM), 117 Test camera (Server ROOM)' :

```bash
een vehiclelist add --name 'vehiclelist test' --camera '108 Test camera (RMA ROOM), 117 Test camera (Server ROOM)'
```

#### Output

**Successful Output Example:**

```text
successfully added vehiclelist: (id: dd5b1209-408d-4c13-aaa5-85da4a4719ba)
```

**Error Output Example:**

```text
unable to add vehiclelist: name already exists (status: 409)
```

### delete

Delete a vehiclelist.

#### Usage:

```
een vehiclelist delete [options] [general options]
```

#### Options:

- `--id [id]`
  Specify id of the vehiclelist to delete.
- `--name [name]`
  Specify name of the vehiclelist to delete.

#### EXAMPLES

- To delete a vehiclelist with name 'test':

```bash
een vehiclelist delete --name 'test'
```

#### Output

**Successful Output Example:**

```text
successfully deleted the vehiclelist: 92cb225e-0c6a-4599-80e4-76b01ecd9c09
```

**Error Output Example:**

```text
error: unable to delete the vehiclelist: resource not found (status: 404)
```

#### Notes:

- Either --name or --id option must be provided.

### list

List all vehiclelist

#### Usage:

```
een vehiclelist list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. Supported values: id, name.
- `-l, --long`
  Display details of vehicles, including camera names, site names, notes.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera ESNs.
- `--name [name]`
  Filter by vehiclelist name.
- `--plate [plate]`
  Filter by license plate number
- `--site [site name1, site name2]`
  Filter by site names.
- `--site-id [site id1, site id2]`
  Filter by site IDs.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

## EXAMPLES

- To get vehiclelist list in CSV format with header:

```bash
een vehiclelist list --csv --header
```

#### Output

```csv
"id","name","status","vehicle count","camera count","site count"
"406cdb01-3383-44d9-8884-7de9eefd6106","Testtt558","active","","12",""
"2ae96131-707a-46b3-ac87-5bcb427e9141","Test1234","active","1","12",""
"9ac3a7a6-040c-4e17-8f1f-632da3c1b0fc","Test0933","active","","12",""
```

- To get vehiclelist list for esn '1234' with vehiclelist name 'my name' in CSV format with headers as long list:

```bash
een vehiclelist list --csv --header -l --esn '1006b36f' --name 'EEN India North'
```

#### Output

```csv
"id","name","status","vehicle count","camera count","site count","camera name","site name","notes"
"416d8e21-a6f0-4b02-93a7-07cd01a9effa","EEN India North","active","19","1","2","108 Test camera (RMA ROOM)","Eagle Eye Bangalor,Eagle Eye India 1","EEN India office North road side facing camera"
```

### set

Update vehiclelist.

#### DESCRIPTION

The `vehiclelist set` command allows you to update the vehiclelist for the specified id.
You can specify the id or name of vehiclelist to change as options and specify options to change.

#### Usage:

```
een vehiclelist set [options] [general options]
```

#### Options:

- `--camera [camera1, camera2]`
  Specify camera names.
- `--disable`
  Set the vehiclelist status to disabled.
- `--enable`
  Set the vehiclelist status to enabled.
- `--esn [esn1, esn2]`
  Specify camera esns.
- `--id [id]`
  Specify id of the vehiclelist to update.
- `--name [name]`
  Specify name of the vehiclelist to update.
- `--new-name [new name]`
  Specify the new name to update the vehiclelist.
- `--notes [notes]`
  Specify notes.

#### EXAMPLES

- To update vehiclelist with name 'Name check list ' to set the name as 'Name Check Vehiclelist' and disable the vehiclelist:

```bash
een vehiclelist set --name 'Name check list' --new-name 'Name Check Vehiclelist' --disable
```

#### Output

**Successful Output Example:**

```text
successfully updated the vehiclelist: (id: 4879606b-1b89-4c74-8080-25cbf93faffc)
```

**Error Output Example:**

```text
unable to update vehiclelist: 100f5b5fga is not a valid camera (status: 400)
```

## Notes:

- Either --name or --id option and at least one option to update must be provided.

---

# vehicle - Manage Vehicle

## NAME

`vehicle` - manage and interact with vehicles.

## SYNOPSIS

```
een vehicle [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `vehicle` command allows you to manage vehicle and list all vehicles.

## COMMANDS

### add

Add vehicle to vehiclelist.

#### Usage:

```
een vehicle add [options] [general options]
```

#### Required Options:

- `--access-type [access-type]`
  Specify access type (supported values: allow, deny).
- `--plate [plate]`
  Specify license plate number.

#### Options:

- `--color [color]`
  Specify color.
- `--make [make]`
  Specify make.
- `--model [model]`
  Specify model.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours).
- `--tag [tag1, tag2]`
  Specify tag.
- `--valid-from [valid-from]`
  Specify date from which this record is valid (supported format: YYYYMMDDhhmmss.sss).
- `--valid-to [valid-to]`
  Specify date up to which this record is valid (supported format: YYYYMMDDhhmmss.sss).
- `--vehiclelist-id [id]`
  Specify vehiclelist id to add vehicle to.
- `--vehiclelist-name [name]`
  Specify vehiclelist name to add vehicle to.

#### EXAMPLES

- To add a vehicle to vehiclelist with id 1234 access type 'allow' plate number 'ABCDK7' make 'acura' color 'white':

```bash
een vehicle add --access-type allow --plate 'ABCDK7' --vehiclelist-id 'd9e9742c-9522-49e8-bb86-ed7eeb4aa14e' --make acura --color white
```

#### Output

**Successful Output Example:**

```text
successfully added vehicle to the vehiclelist: (id: 06c0c857-07ed-4885-9fe9-9cbf4bee1560)
```

**Error Output Example:**

```text
unable to add vehicle to the vehiclelist: plate already exists (status: 409)
```

### delete

Delete a vehicle from vehiclelist.

#### Usage:

```
een vehicle delete [options] [general options]
```

#### Options:

- `--plate [plate]`
  Specify license plate number of the vehicle to delete.
- `--vehicle-id [id]`
  Specify id of the vehicle to delete.
- `--vehiclelist-id [id]`
  Specify id of the vehiclelist to delete the vehicle from.
- `--vehiclelist-name [name]`
  Specify name of the vehiclelist to delete the vehicle from.

#### EXAMPLES

- To delete a vehicle with plate number 'YUIOPT' from vehiclelist with name 'een north':

```bash
een vehicle delete --plate 'YUIOPT' --vehiclelist-name 'een north'
```

#### Output

**Successful Output Example:**

```text
successfully deleted the vehicle: 8b741095-89fd-420c-93e7-ca2914107761 from the vehiclelist d9e9742c-9522-49e8-bb86-ed7eeb4aa14e
```

**Error Output Example:**

```text
error: unable to delete the vehicle from vehiclelist: resource not found (status: 404)
```

## Notes:

- Either --vehiclelist-name or --vehiclelist-id option must be provided.
- Either --plate or --vehicle-id option must be provided.

### list

List details of vehicle

#### Usage:

```
een vehicle list [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `--id [id]`
  Display details of vehicles with the specified vehiclelist id.
- `--include [value1, value2]`
  Display associated items. Supported values: id, plate.
- `-l, --long`
  Display details of vehicles, including vehicle id, color, make, model, user tags, security status, vehiclelist id.
- `--name [name]`
  Display details of vehicles with the specified vehiclelist name.

#### Selectors:

- `--access-type [type1, type2]`
  Filter by access type (supported values: allow, deny).
- `--plate [plate]`
  Filter by license plate number.
- `--user-tags [tag1, tag2]`
  Filter by user tags.

## EXAMPLES

- To get VSP list vehicles with vehiclelist name 'Hotlist Vehicles' in CSV format with header:

```bash
een vehicle list --name 'Hotlist Vehicles' --csv --header
```

#### Output

```csv
"license plate","access type","valid from","valid to","user data","vehiclelist name"
"LHS7593","allow","","","","Hotlist Vehicles"
"SMY5299","allow","","","","Hotlist Vehicles"
"GZJ8668","allow","","","","Hotlist Vehicles"
```

- To get VSP list vehicles with vehiclelist id '23j2j5' and user tags 'brivo' in CSV format with headers as long list:

```bash
een vehicle list --id 'e705d1f9-4846-4c98-aa09-20b5e54b694f' -l --header  --user-tags 'brivo' --csv
```

#### Output

```csv
"license plate","access type","valid from","valid to","user data","vehiclelist name","id","color","make","model","user tags","security status","vehiclelist id"
"VPM1767","allow","","","emp_id/1028, company/brivo","Employee List","ff149647-7146-4dd1-ba6a-a55640f53f29","","","","emp_id,1028,company,brivo","exempted","e705d1f9-4846-4c98-aa09-20b5e54b694f"
"TKN9576","allow","","","emp_id/1007, company/brivo","Employee List","fc540121-cb52-4fd9-b9ce-bc3abd43a7e1","","","","emp_id,1007,company,brivo","exempted","e705d1f9-4846-4c98-aa09-20b5e54b694f"
```

- To get VSP list vehicles with vehiclelist name 'hotlist' and license plate number 'NJIFUI7' in CSV format with headers as long list:

```bash
een vehicle list --name 'Hotlist Vehicles'  -l --header  --plate 'PSM1356' --csv
```

#### Output

```csv
"license plate","access type","valid from","valid to","user data","vehiclelist name","id","color","make","model","user tags","security status","vehiclelist id"
"PSM1356","allow","","","","Hotlist Vehicles","f34478ea-46f5-4423-b5a0-23bbe5ad19f0","","","","","","3539f639-00d1-4c6b-b1a7-c66954f4cb93"
```

### set

Update vehicle details.

#### Usage:

```
een vehicle set [options] [general options]
```

#### Options:

- `--access-type [access-type]`
  Specify access type (supported values: allow, deny).
- `--color [color]`
  Specify color.
- `--make [make]`
  Specify make.
- `--model [model]`
  Specify model.
- `--plate [plate]`
  Specify license plate number of the vehicle to update.
- `--schedule [schedule]`
  Specify schedule (supported values: workHours, nonWorkHours, fullHours).
- `--tag [tag1, tag2]`
  Specify tag.
- `--valid-from [valid-from]`
  Specify date from which this record is valid (supported format: YYYYMMDDhhmmss.sss).
- `--valid-to [valid-to]`
  Specify date up to which this record is valid (supported format: YYYYMMDDhhmmss.sss).
- `--vehicle-id [id]`
  Specify id of the vehicle to update.
- `--vehiclelist-id [id]`
  Specify id of the vehiclelist to update the vehicle from.
- `--vehiclelist-name [name]`
  Specify name of the vehiclelist to update the vehicle from.

#### EXAMPLES

- To update vehicle with plate number 'QWERTY' from the vehiclelist 'New_Vehicle list_1901' to set the access type as 'allow' and valid from to '2026-04-01':

```bash
een vehicle set --plate 'QWERTY' --vehiclelist-name 'New_Vehicle list_1901' --access-type 'allow' --valid-from '20260401000000.000'
```

#### Output

**Successful Output Example:**

```text
successfully updated vehicle details: (id: d32c71fd-0b47-4da7-9716-e2cfca5e519f)
```

**Error Output Example:**

```text
error: unable to update vehicle details: validfrom must be less than validto (status: 400)
```

## Notes:

- Either --vehiclelist-name or --vehiclelist-id option must be provided.
- Either --plate or --vehicle-id option must be provided.

---

# pos - Manage Point of Sale (POS) Events

## NAME

`pos` - manage and retrieve Point of Sale events.

## SYNOPSIS

```
een pos [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `pos` command allows you to manage and retrieve POS events based on parameters such as time, transaction details, and site.

## COMMANDS

### listevents

Get point of sale (POS) events.

#### Usage:

```
een pos listevents [options] [selectors] [general options]
```

#### Options:

- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify events end time; ensure that the --start-time option is used.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.
- `--html`
  Generate chart in HTML file.
- `-s, --start-time [start time]`
  Specify events start time.

#### Selectors:

- `-b, --bill-number [bill number]`
  Filter by bill number.
- `--discount-max [discount max]`
  Filter by maximum discount.
- `--discount-min [discount min]`
  Filter by minimum discount.
- `-E, --employee-id [employee ID]`
  Filter by employee ID.
- `-F, --flagged`
  Filter by flagged transactions.
- `--net-amount-max [net amount max]`
  Filter by maximum net amount.
- `--net-amount-min [net amount min]`
  Filter by minimum net amount.
- `--site [site name1, site name2]`
  Filter by site names associated with the camera.
- `--site-id [site id1, site id2]`
  Filter by site IDs associated with the camera.
- `-t, --transaction-type [transaction type]`
  Filter by type of the transaction.

#### Notes:

- If no start time or end time is specified, the retrieval period defaults to the last 24 hours.

#### Actions:

- If `--html` is specified, it generates a report of POS events.
- If not, it retrieves POS events and saves them according to the specified options.

## EXAMPLES

- To get POS events for a specific time frame:

```bash
een pos listevents --start-time 2024-11-17T09:20:54.619+00:00 --end-time 2024-11-18T09:20:54.619+00:00
```

- To get flagged POS transactions:

```bash
een pos listevents --flagged
```

---

# perftest - Execute Performance Tests

## NAME

`perftest` - execute performance tests.

## SYNOPSIS

```
een perftest [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `perftest` command allows you to execute performance tests on various aspects of the platform.

## COMMAND

### livelatency

#### Usage:

```
een perftest livelatency [options] [selectors] [general options]
```

## Example

To get camera perftest livelatency for all cameras in CSV format (with headers):

```bash
een perftest livelatency --header --csv
```

#### Output:

```
account: Account_name(00244829)

running livelatency performance test for 10 samples on 1 cameras

tested camera test-camera-1 (1003d9df)... min: 5312.00ms, max: 9149.00ms, avg: 8464.40ms

perftest livelatency run on 1/1 cameras 10 samples each

"bridge","camera","minimum time (ms)","maximum time (ms)","average time (ms)"
"test-camera-1(100236d0)","DB14-GUN(1003d9df)","5312.00","9149.00","8464.40"

```

### preview

Get performance test results for preview images.

#### Usage:

```
een perftest preview [options] [selectors] [general options]
```

#### Options:

- `-a, --all-log`
  Display execution logs.
- `-c, --count [count]`
  Specify number of previews to be tested (default: 10).
- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `--fixed`
  Generate timestamps at fixed intervals (interval: 10000 ms).
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `-s, --start-time [start time]`
  Specify the start timestamp for analysis.
- `--v1`
  Test performance of the V1 API.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--layout [layout1, layout2]`
  Filter by layouts.
- `--layout-id [layout id1, layout id2]`
  Filter by layouts ids.
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

#### Notes:

- If no start time or end time is specified, the test interval will be last 30 days.
- If the specified time range exceeds the retention period of the camera, the test will be performed over the actual retention period of the camera.

## EXAMPLES

- To test preview performance of all the cameras in an account for last 30 days:

```bash
een perftest preview
```

- To test preview performance of all the cameras in a specific layout:

```bash
een perftest preview --layout "layout1"
```

- To test preview performance of all the cameras in a specific site:

```bash
een perftest preview --site "site1"
```

### assetlist

Get performance test results for asset list endpoint.

#### Usage:

```
een perftest assetlist [options] [selectors] [general options]
```

#### Options:

- `-a, --all-log`
  Display execution logs.
- `-A, --asset-count [asset count]`
  Specify number of assets per list (default: 10).
- `--archiver`
  Display the archiver id.
- `-c, --count [count]`
  Specify number of asset lists to be tested (default: 10).
- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `--fixed`
  Generate timestamps at fixed intervals (interval: 10000 ms).
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `-H, --headerinfo`
  Display response header info.
- `--header`
  Display column headers in the result.
- `-s, --start-time [start time]`
  Specify the start timestamp for analysis.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--layout [layout1, layout2]`
  Filter by layouts.
- `--layout-id [layout id1, layout id2]`
  Filter by layouts ids.
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

#### Notes:

- If no start time or end time is specified, the test interval will be last 30 days.

## EXAMPLES

- To test asset list performance of all the cameras in an account for last 30 days:

```bash
een perftest assetlist
```

```bash
een perftest assetlist --layout "layout1"
```

- To test asset list performance of all the cameras in a specific site:

```bash
een perftest assetlist --site "site1"
```

### pngspan

Get performance test results for pngspan endpoint.

#### Usage:

```
een perftest pngspan [options] [selectors] [general options]
```

#### Options:

- `-a, --all-log`
  Display execution logs.
- `--archiver`
  Display the archiver ID.
- `-c, --count [count]`
  Specify number of pngspans to be tested (default: 10).
- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `--fixed`
  Generate timestamps at fixed intervals (interval: 10000 ms).
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `-H, --headerinfo`
  Display response header info.
- `--header`
  Display column headers in the result.
- `-s, --start-time [start time]`
  Specify the start timestamp for analysis.
- `--width [width]`
  Specify width of pngspan to be tested (default: 240).

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--layout [layout1, layout2]`
  Filter by layouts.
- `--layout-id [layout id1, layout id2]`
  Filter by layouts ids.
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

#### Notes:

- If no start time or end time is specified, the test interval will be last 30 days.
- If the specified time range exceeds the retention period of the camera, the test will be performed over the actual retention period of the camera.

## EXAMPLES

- To test pngspan performance of all the cameras in an account for last 30 days:

```bash
een perftest pngspan
```

- To test pngspan performance of all the cameras in a specific layout:

```bash
een perftest pngspan --layout "layout1"
```

- To test pngspan performance of all the cameras in a specific site:

```bash
een perftest pngspan --site "site1"
```

### live

Get performance test results for live video.

#### Usage:

```
een perftest live [options] [selectors] [general options]
```

#### Options:

- `-a, --all-log`
  Display execution logs.
- `-c, --count [count]`
  Specify number of videos to be tested (default: 10).
- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `-l, --length [length]`
  Specify the video duration for analysis (default: 10s).

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--layout [layout1, layout2]`
  Filter by layouts.
- `--layout-id [layout id1, layout id2]`
  Filter by layouts ids.
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`  
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

## EXAMPLES

- To test live video performance of all the cameras in an account:

```bash
een perftest live
```

- To test live video performance of all the cameras in a specific layout:

```bash
een perftest live --layout "layout1"
```

- To test live video performance of all the cameras in a specific site:

```bash
een perftest live --site "site1"
```

### livelatency

Get test results live video latency

#### Usage:

```
een perftest livelatency [options] [selectors] [general options]
```

#### Options:

- `-a, --all-log`
  Display execution logs.
- `-c, --count [count]`
  Specify number of videos frames to be tested (default: 10).
- `--csv`
  Display details in CSV format.
- `-f, --file-name [file name]`
  Specify the file name to save the test results.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--layout [layout1, layout2]`
  Filter by layouts.
- `--layout-id [layout id1, layout id2]`
  Filter by layouts ids.
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

## EXAMPLES

- To test live video latency of all the cameras in an account:

```bash
een perftest livelatency
```

- To test live video latency of all the cameras in a specific bridge:

```bash
een perftest livelatency --bridge-esn "<bridge_id>"
```

### historic

Get performance test results for history video.

#### Usage:

```
een perftest historic [options] [selectors] [general options]
```

#### Options:

- `-a, --all-log`
  Display execution logs.
- `-c, --count [count]`
  Specify number of videos to be tested (default: 10).
- `--csv`
  Display details in CSV format.
- `-e, --end-time [end time]`
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `--fixed`
  Generate timestamps at fixed intervals.
- `-g, --google-sheet`
  Display details in CSV format in google sheet.
- `--header`
  Display column headers in the result.
- `-l, --length [video length]`
  Specify the video duration for analysis (default: 10s).
- `-s, --start-time [start time]`
  Specify the start timestamp for analysis.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter by bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esns.
- `-C, --camera [camera1, camera2]`
  Filter by cameras.
- `--esn [esn1, esn2]`
  Filter by camera esns.
- `--layout [layout1, layout2]`
  Filter by layouts.
- `--layout-id [layout id1, layout id2]`
  Filter by layouts ids.
- `--site [site1, site2]`
  Filter by sites.
- `--site-id [site id1, site id2]`
  Filter by site ids.
- `--status [status]`
  Filter by camera status.
- `-t, --tag [tag1, tag2]`
  Filter by tags.

#### Notes:

- If no start time or end time is specified, the test interval will be last 30 days.
- If the specified time range exceeds the retention period of the camera, the test will be performed over the actual retention period of the camera.

## EXAMPLES

- To test history video performance of all the cameras in an account for last 30 days:

```bash
een perftest historic
```

- To test history video performance of all the cameras in a specific layout:

```bash
een perftest historic --layout "layout1"
```

- To test history video performance of all the cameras in a specific site:

```bash
een perftest historic --site "site1"
```

---

# googleconfig - Update Google Configuration Options

## NAME

`googleconfig` - update configuration options for Google settings.

## SYNOPSIS

```
een googleconfig update <option name> <value>
```

## DESCRIPTION

The `googleconfig` command allows you to update specific configuration options related to Google settings.

#### Usage:

```
een googleconfig [options] [command]
```

## COMMANDS

### update

Update Google config option values.

#### Usage:

```
een googleconfig update [options] <option name> <value>
```

#### Arguments:

- `<option name>`
  The name of the configuration option that needs to be updated.

- `<value>`
  The new value for the specified option. This value is parsed as a JSON string.

#### Action:

The action processes the provided option name and value, parsing the value as JSON and updating the Google configuration file accordingly.

## EXAMPLES

To update a Google configuration option:

```bash
een googleconfig update "api_key" "your_api_key_value"
```

# For Google Sheets commands

#### Generate Credentials for accessing Google Sheets and Google Drive

[Google Cloud Console](https://console.cloud.google.com/)

The credentials required depends on the type of data, platform, and access methodology of your app.

#### Create a service account

1. Open the Google Cloud console.

[Google Cloud Console](https://console.cloud.google.com/)

2. At the top-left, click Menu menu > IAM & Admin > Service Accounts.
3. Click Create service account.
4. Fill in the service account details, then click Create and continue.
5. Optional: Assign roles to your service account to grant access to your Google Cloud project's resources.
6. Click Continue.
7. Optional: Enter users or groups that can manage and perform actions with this service account.
8. Click Done.

### Service account

Use this credential to authenticate as a robot service account or to access resources on behalf of Google Workspace or Cloud Identity users through domain-wide delegation.

#### Create credentials for a service account

You need to obtain credentials in the form of a public/private key pair. These credentials are used by your code to authorize service account actions within your app.

#### To obtain credentials for your service account:

1. Open the Google Cloud console.

[Google Cloud Console](https://console.cloud.google.com/)

2. At the top-left, click Menu menu > IAM & Admin > Service Accounts.
3. Select your service account.
4. Click Keys > Add keys > Create new key.
5. Select JSON, then click Create.
   Your new public/private key pair is generated and downloaded to your machine as a new file. This file is the only copy of this key.
6. Click Close.

#### Drive Folder ID

A folder ID can be extracted from its URL. For example, the folder ID in the URL https://drive.google.com/drive/folders/ABCDE12345 is `ABCDE12345`.

#### Grant Editor permission to access the Google Drive folder

Grant permission to your client email in your Google Drive folder.
Client email is the email that you get while initializing the project in the Google Cloud console.

### IMPORTANT:

#### Enable GoogleSheet API and Google Drive APIs

1. Open APIS and Services page

[APIS and Services](https://console.cloud.google.com/apis)

2. Navigate to API Library

[API Library](https://console.cloud.google.com/apis/library)

3. Search for Google Drive API

[Google Drive API](https://console.cloud.google.com/apis/library/drive.googleapis.com)

4. Enable Google Drive API by clicking on the `ENABLE` button

5. Search for Google Sheets API

[Google Sheets API](https://console.cloud.google.com/apis/library/sheets.googleapis.com)

6. Enable Google Sheets API by clicking on the `ENABLE` button

### Note:

While executing Google Sheets commands, if you encounter any error messages like:

```
 errors: [
    {
      message: 'Google Sheets API has not been used in project 886039128663 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/sheets.googleapis.com/overview?project=886039128663 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.',
      domain: 'usageLimits',
      reason: 'accessNotConfigured',
      extendedHelp: 'https://console.developers.google.com'
    }
  ]

```

This error indicates that you are not `enabled` Google Sheets API for your service account.

```
errors: [
   {
     message: 'Google Drive API has not been used in project 886039128663 before or it is disabled. Enable it by visiting https://console.developers.google.com/apis/api/drive.googleapis.com/overview?project=886039128663 then retry. If you enabled this API recently, wait a few minutes for the action to propagate to our systems and retry.',
     domain: 'usageLimits',
     reason: 'accessNotConfigured',
     extendedHelp: 'https://console.developers.google.com'
   }
 ]

```

This error indicates that you are not `enabled` Google Drive API for your service account.

To fix the same, please follow the steps above for enabling GoogleSheet API and Google Drive API

#### Setting Google Configuration

The .een/static_config.json file that gets created while logging in using the CLI has the following values:

- "serviceAccountPrivateKey": "your private key"
- "serviceAccountClientEmail": "your client email"
- "driveFolderID": "google drive folder id"

The serviceAccountPrivateKey and serviceAccountClientEmail can be found in your downloaded file, you get while doing the step 5 in obtaining the credentials for your service account.

Replace these values with your credentials, you will be able to get the Google Sheets commands working.

#### To update the Google config values, you can also use the command:

```
een googleconfig update <name> -- <value>
```

Example:

```
een googleconfig update "driveFolderID" -- "1giou_ghlihbZyUpwCx"
```

---

### Output Formats and Options

#### Using `--include` to Select Fields

Many commands support the `--include` option to display only specific fields in the output. This allows you to customize the data returned for easier parsing and processing.

**Examples:**

```bash
# Get only camera ESNs in camera list
een camera list --include 'esn'

# Get only bridge ESNs in bridge list
een bridge list --include 'esn'
```

When using the `--include` option, only the specified fields will be returned in the output.

---

#### Output Formats

The EEN CLI tool supports three main output formats. By default, headers are hidden in all formats unless `--header` is specified.

1. **Table Format (Default)**
   Human-readable output in a table format.

   ```bash
   # Table output (headers hidden)
   een camera list

   # Table output with headers
   een camera list --header
   ```

2. **CSV Format**
   Comma-separated values for data processing.

   ```bash
   # CSV output without headers
   een camera list --csv

   # CSV output with headers
   een camera list --csv --header
   ```

3. **Google Sheets Format**
   Uploads the output to a Google Sheet in your configured Google account.

   ```bash
   # Google Sheets output without headers
   een camera list --google-sheet

   # Google Sheets output with headers
   een camera list --google-sheet --header
   ```

---

#### Prompt Handling (`--prompt` option)

The `--prompt` option adds confirmation prompts during command execution for safety-critical operations, such as overwriting files.

**Example:**

```bash
# File overwrite prompt
een camera list --csv --file-name cameras.csv --prompt
# Output: File 'cameras.csv' already exists. Overwrite? (y/N):
```

---

#### Error Handling

All error messages are printed to stderr, and successful data is printed to stdout, making it easy to parse and process results in scripts.

---

#### API Versions

The EEN CLI tool supports two API versions:

- **v3 API (Default):** All commands use v3 APIs by default (recommended).
- **v1 API (Legacy):** Some commands support the legacy v1 API using the `--v1` option.

**Usage v1 APIs:**

```bash
# Using default v3 API
een camera list

# Using v1 API
een camera list --v1
```

**Commands Supporting `--v1`:**

- `user list`
- `camera list`
- `camera settings`
- `bridge list`
- `lpr events`
- `perftest preview`

---

#### Available Status Values

**Camera status for v1:**

- Camera online
- Stream attached
- Camera on
- Camera recording
- Camera sending previews
- Camera located
- Camera not supported
- Camera configuration in process
- Camera needs ONVIF password
- Camera available but not yet attached
- Internal status
- Camera error
- Reserved
- Invalid state
- Camera streaming
- Camera registered

**Device status for v3 (camera, bridge, etc.):**

- online
- deviceOffline
- invalidCredentials
- bridgeOffline
- off
- offline
- error
- unknown

---

#### Important Note about Comma-Separated Values:

When passing multiple values separated by commas to any option, always use **single quotes** to prevent shell interpretation issues.

**Correct:**:

```bash
een camera list --esn 'cam1,cam2,cam3'
een bridge list --site 'Site A,Site B,Site C'
een user list --include 'email,firstname,lastname'
```

**Avoid:**:

```bash
een camera list --esn cam1,cam2,cam3          # May not work - shell splits on commas
een camera list --esn "cam1,cam2,cam3"        # May work but can cause issues in some cases
```

### Available timezones

- "Africa/Abidjan"
- "Africa/Accra"
- "Africa/Addis_Ababa"
- "Africa/Algiers"
- "Africa/Asmara"
- "Africa/Asmera"
- "Africa/Bamako"
- "Africa/Bangui"
- "Africa/Banjul"
- "Africa/Bissau"
- "Africa/Blantyre"
- "Africa/Brazzaville"
- "Africa/Bujumbura"
- "Africa/Cairo"
- "Africa/Casablanca"
- "Africa/Ceuta"
- "Africa/Conakry"
- "Africa/Dakar"
- "Africa/Dar_es_Salaam"
- "Africa/Djibouti"
- "Africa/Douala"
- "Africa/El_Aaiun"
- "Africa/Freetown"
- "Africa/Gaborone"
- "Africa/Harare"
- "Africa/Johannesburg"
- "Africa/Juba"
- "Africa/Kampala"
- "Africa/Khartoum"
- "Africa/Kigali"
- "Africa/Kinshasa"
- "Africa/Lagos"
- "Africa/Libreville"
- "Africa/Lome"
- "Africa/Luanda"
- "Africa/Lubumbashi"
- "Africa/Lusaka"
- "Africa/Malabo"
- "Africa/Maputo"
- "Africa/Maseru"
- "Africa/Mbabane"
- "Africa/Mogadishu"
- "Africa/Monrovia"
- "Africa/Nairobi"
- "Africa/Ndjamena"
- "Africa/Niamey"
- "Africa/Nouakchott"
- "Africa/Ouagadougou"
- "Africa/Porto-Novo"
- "Africa/Sao_Tome"
- "Africa/Timbuktu"
- "Africa/Tripoli"
- "Africa/Tunis"
- "Africa/Windhoek"
- "America/Adak"
- "America/Anchorage"
- "America/Anguilla"
- "America/Antigua"
- "America/Araguaina"
- "America/Argentina/Buenos_Aires"
- "America/Argentina/Catamarca"
- "America/Argentina/ComodRivadavia"
- "America/Argentina/Cordoba"
- "America/Argentina/Jujuy"
- "America/Argentina/La_Rioja"
- "America/Argentina/Mendoza"
- "America/Argentina/Rio_Gallegos"
- "America/Argentina/Salta"
- "America/Argentina/San_Juan"
- "America/Argentina/San_Luis"
- "America/Argentina/Tucuman"
- "America/Argentina/Ushuaia"
- "America/Aruba"
- "America/Asuncion"
- "America/Atikokan"
- "America/Atka"
- "America/Bahia"
- "America/Bahia_Banderas"
- "America/Barbados"
- "America/Belem"
- "America/Belize"
- "America/Blanc-Sablon"
- "America/Boa_Vista"
- "America/Bogota"
- "America/Boise"
- "America/Buenos_Aires"
- "America/Cambridge_Bay"
- "America/Campo_Grande"
- "America/Cancun"
- "America/Caracas"
- "America/Catamarca"
- "America/Cayenne"
- "America/Cayman"
- "America/Chicago"
- "America/Chihuahua"
- "America/Coral_Harbour"
- "America/Cordoba"
- "America/Costa_Rica"
- "America/Creston"
- "America/Cuiaba"
- "America/Curacao"
- "America/Danmarkshavn"
- "America/Dawson"
- "America/Dawson_Creek"
- "America/Denver"
- "America/Detroit"
- "America/Dominica"
- "America/Edmonton"
- "America/Eirunepe"
- "America/El_Salvador"
- "America/Ensenada"
- "America/Fort_Nelson"
- "America/Fort_Wayne"
- "America/Fortaleza"
- "America/Glace_Bay"
- "America/Godthab"
- "America/Goose_Bay"
- "America/Grand_Turk"
- "America/Grenada"
- "America/Guadeloupe"
- "America/Guatemala"
- "America/Guayaquil"
- "America/Guyana"
- "America/Halifax"
- "America/Havana"
- "America/Hermosillo"
- "America/Indiana/Indianapolis"
- "America/Indiana/Knox"
- "America/Indiana/Marengo"
- "America/Indiana/Petersburg"
- "America/Indiana/Tell_City"
- "America/Indiana/Vevay"
- "America/Indiana/Vincennes"
- "America/Indiana/Winamac"
- "America/Indianapolis"
- "America/Inuvik"
- "America/Iqaluit"
- "America/Jamaica"
- "America/Jujuy"
- "America/Juneau"
- "America/Kentucky/Louisville"
- "America/Kentucky/Monticello"
- "America/Knox_IN"
- "America/Kralendijk"
- "America/La_Paz"
- "America/Lima"
- "America/Los_Angeles"
- "America/Louisville"
- "America/Lower_Princes"
- "America/Maceio"
- "America/Managua"
- "America/Manaus"
- "America/Marigot"
- "America/Martinique"
- "America/Matamoros"
- "America/Mazatlan"
- "America/Mendoza"
- "America/Menominee"
- "America/Merida"
- "America/Metlakatla"
- "America/Mexico_City"
- "America/Miquelon"
- "America/Moncton"
- "America/Monterrey"
- "America/Montevideo"
- "America/Montreal"
- "America/Montserrat"
- "America/Nassau"
- "America/New_York"
- "America/Nipigon"
- "America/Nome"
- "America/Noronha"
- "America/North_Dakota/Beulah"
- "America/North_Dakota/Center"
- "America/North_Dakota/New_Salem"
- "America/Ojinaga"
- "America/Panama"
- "America/Pangnirtung"
- "America/Paramaribo"
- "America/Phoenix"
- "America/Port-au-Prince"
- "America/Port_of_Spain"
- "America/Porto_Acre"
- "America/Porto_Velho"
- "America/Puerto_Rico"
- "America/Punta_Arenas"
- "America/Rainy_River"
- "America/Rankin_Inlet"
- "America/Recife"
- "America/Regina"
- "America/Resolute"
- "America/Rio_Branco"
- "America/Rosario"
- "America/Santa_Isabel"
- "America/Santarem"
- "America/Santiago"
- "America/Santo_Domingo"
- "America/Sao_Paulo"
- "America/Scoresbysund"
- "America/Shiprock"
- "America/Sitka"
- "America/St_Barthelemy"
- "America/St_Johns"
- "America/St_Kitts"
- "America/St_Lucia"
- "America/St_Thomas"
- "America/St_Vincent"
- "America/Swift_Current"
- "America/Tegucigalpa"
- "America/Thule"
- "America/Thunder_Bay"
- "America/Tijuana"
- "America/Toronto"
- "America/Tortola"
- "America/Vancouver"
- "America/Virgin"
- "America/Whitehorse"
- "America/Winnipeg"
- "America/Yakutat"
- "America/Yellowknife"
- "Antarctica/Casey"
- "Antarctica/Davis"
- "Antarctica/DumontDUrville"
- "Antarctica/Macquarie"
- "Antarctica/Mawson"
- "Antarctica/McMurdo"
- "Antarctica/Palmer"
- "Antarctica/Rothera"
- "Antarctica/South_Pole"
- "Antarctica/Syowa"
- "Antarctica/Troll"
- "Antarctica/Vostok"
- "Arctic/Longyearbyen"
- "Asia/Aden"
- "Asia/Almaty"
- "Asia/Amman"
- "Asia/Anadyr"
- "Asia/Aqtau"
- "Asia/Aqtobe"
- "Asia/Ashgabat"
- "Asia/Ashkhabad"
- "Asia/Atyrau"
- "Asia/Baghdad"
- "Asia/Bahrain"
- "Asia/Baku"
- "Asia/Bangkok"
- "Asia/Barnaul"
- "Asia/Beirut"
- "Asia/Bishkek"
- "Asia/Brunei"
- "Asia/Calcutta"
- "Asia/Chita"
- "Asia/Choibalsan"
- "Asia/Chongqing"
- "Asia/Chungking"
- "Asia/Colombo"
- "Asia/Dacca"
- "Asia/Damascus"
- "Asia/Dhaka"
- "Asia/Dili"
- "Asia/Dubai"
- "Asia/Dushanbe"
- "Asia/Famagusta"
- "Asia/Gaza"
- "Asia/Harbin"
- "Asia/Hebron"
- "Asia/Ho_Chi_Minh"
- "Asia/Hong_Kong"
- "Asia/Hovd"
- "Asia/Irkutsk"
- "Asia/Istanbul"
- "Asia/Jakarta"
- "Asia/Jayapura"
- "Asia/Jerusalem"
- "Asia/Kabul"
- "Asia/Kamchatka"
- "Asia/Karachi"
- "Asia/Kashgar"
- "Asia/Kathmandu"
- "Asia/Katmandu"
- "Asia/Khandyga"
- "Asia/Kolkata"
- "Asia/Krasnoyarsk"
- "Asia/Kuala_Lumpur"
- "Asia/Kuching"
- "Asia/Kuwait"
- "Asia/Macao"
- "Asia/Macau"
- "Asia/Magadan"
- "Asia/Makassar"
- "Asia/Manila"
- "Asia/Muscat"
- "Asia/Nicosia"
- "Asia/Novokuznetsk"
- "Asia/Novosibirsk"
- "Asia/Omsk"
- "Asia/Oral"
- "Asia/Phnom_Penh"
- "Asia/Pontianak"
- "Asia/Pyongyang"
- "Asia/Qatar"
- "Asia/Qostanay"
- "Asia/Qyzylorda"
- "Asia/Rangoon"
- "Asia/Riyadh"
- "Asia/Saigon"
- "Asia/Sakhalin"
- "Asia/Samarkand"
- "Asia/Seoul"
- "Asia/Shanghai"
- "Asia/Singapore"
- "Asia/Srednekolymsk"
- "Asia/Taipei"
- "Asia/Tashkent"
- "Asia/Tbilisi"
- "Asia/Tehran"
- "Asia/Tel_Aviv"
- "Asia/Thimbu"
- "Asia/Thimphu"
- "Asia/Tokyo"
- "Asia/Tomsk"
- "Asia/Ujung_Pandang"
- "Asia/Ulaanbaatar"
- "Asia/Ulan_Bator"
- "Asia/Urumqi"
- "Asia/Ust-Nera"
- "Asia/Vientiane"
- "Asia/Vladivostok"
- "Asia/Yakutsk"
- "Asia/Yangon"
- "Asia/Yekaterinburg"
- "Asia/Yerevan"
- "Atlantic/Azores"
- "Atlantic/Bermuda"
- "Atlantic/Canary"
- "Atlantic/Cape_Verde"
- "Atlantic/Faeroe"
- "Atlantic/Faroe"
- "Atlantic/Jan_Mayen"
- "Atlantic/Madeira"
- "Atlantic/Reykjavik"
- "Atlantic/South_Georgia"
- "Atlantic/St_Helena"
- "Atlantic/Stanley"
- "Australia/ACT"
- "Australia/Adelaide"
- "Australia/Brisbane"
- "Australia/Broken_Hill"
- "Australia/Canberra"
- "Australia/Currie"
- "Australia/Darwin"
- "Australia/Eucla"
- "Australia/Hobart"
- "Australia/LHI"
- "Australia/Lindeman"
- "Australia/Lord_Howe"
- "Australia/Melbourne"
- "Australia/NSW"
- "Australia/North"
- "Australia/Perth"
- "Australia/Queensland"
- "Australia/South"
- "Australia/Sydney"
- "Australia/Tasmania"
- "Australia/Victoria"
- "Australia/West"
- "Australia/Yancowinna"
- "Brazil/Acre"
- "Brazil/DeNoronha"
- "Brazil/East"
- "Brazil/West"
- "CET"
- "CST6CDT"
- "Canada/Atlantic"
- "Canada/Central"
- "Canada/Eastern"
- "Canada/Mountain"
- "Canada/Newfoundland"
- "Canada/Pacific"
- "Canada/Saskatchewan"
- "Canada/Yukon"
- "Chile/Continental"
- "Chile/EasterIsland"
- "Cuba"
- "EET"
- "EST"
- "EST5EDT"
- "Egypt"
- "Eire"
- "Etc/GMT"
- "Etc/GMT+0"
- "Etc/GMT+1"
- "Etc/GMT+10"
- "Etc/GMT+11"
- "Etc/GMT+12"
- "Etc/GMT+2"
- "Etc/GMT+3"
- "Etc/GMT+4"
- "Etc/GMT+5"
- "Etc/GMT+6"
- "Etc/GMT+7"
- "Etc/GMT+8"
- "Etc/GMT+9"
- "Etc/GMT-0"
- "Etc/GMT-1"
- "Etc/GMT-10"
- "Etc/GMT-11"
- "Etc/GMT-12"
- "Etc/GMT-13"
- "Etc/GMT-14"
- "Etc/GMT-2"
- "Etc/GMT-3"
- "Etc/GMT-4"
- "Etc/GMT-5"
- "Etc/GMT-6"
- "Etc/GMT-7"
- "Etc/GMT-8"
- "Etc/GMT-9"
- "Etc/GMT0"
- "Etc/Greenwich"
- "Etc/UCT"
- "Etc/UTC"
- "Etc/Universal"
- "Etc/Zulu"
- "Europe/Amsterdam"
- "Europe/Andorra"
- "Europe/Astrakhan"
- "Europe/Athens"
- "Europe/Belfast"
- "Europe/Belgrade"
- "Europe/Berlin"
- "Europe/Bratislava"
- "Europe/Brussels"
- "Europe/Bucharest"
- "Europe/Budapest"
- "Europe/Busingen"
- "Europe/Chisinau"
- "Europe/Copenhagen"
- "Europe/Dublin"
- "Europe/Gibraltar"
- "Europe/Guernsey"
- "Europe/Helsinki"
- "Europe/Isle_of_Man"
- "Europe/Istanbul"
- "Europe/Jersey"
- "Europe/Kaliningrad"
- "Europe/Kiev"
- "Europe/Kirov"
- "Europe/Lisbon"
- "Europe/Ljubljana"
- "Europe/London"
- "Europe/Luxembourg"
- "Europe/Madrid"
- "Europe/Malta"
- "Europe/Mariehamn"
- "Europe/Minsk"
- "Europe/Monaco"
- "Europe/Moscow"
- "Europe/Nicosia"
- "Europe/Oslo"
- "Europe/Paris"
- "Europe/Podgorica"
- "Europe/Prague"
- "Europe/Riga"
- "Europe/Rome"
- "Europe/Samara"
- "Europe/San_Marino"
- "Europe/Sarajevo"
- "Europe/Saratov"
- "Europe/Simferopol"
- "Europe/Skopje"
- "Europe/Sofia"
- "Europe/Stockholm"
- "Europe/Tallinn"
- "Europe/Tirane"
- "Europe/Tiraspol"
- "Europe/Ulyanovsk"
- "Europe/Uzhgorod"
- "Europe/Vaduz"
- "Europe/Vatican"
- "Europe/Vienna"
- "Europe/Vilnius"
- "Europe/Volgograd"
- "Europe/Warsaw"
- "Europe/Zagreb"
- "Europe/Zaporozhye"
- "Europe/Zurich"
- "Factory"
- "GB"
- "GB-Eire"
- "GMT"
- "GMT+0"
- "GMT-0"
- "GMT0"
- "Greenwich"
- "HST"
- "Hongkong"
- "Iceland"
- "Indian/Antananarivo"
- "Indian/Chagos"
- "Indian/Christmas"
- "Indian/Cocos"
- "Indian/Comoro"
- "Indian/Kerguelen"
- "Indian/Mahe"
- "Indian/Maldives"
- "Indian/Mauritius"
- "Indian/Mayotte"
- "Indian/Reunion"
- "Iran"
- "Israel"
- "Jamaica"
- "Japan"
- "Kwajalein"
- "Libya"
- "MET"
- "MST"
- "MST7MDT"
- "Mexico/BajaNorte"
- "Mexico/BajaSur"
- "Mexico/General"
- "NZ"
- "NZ-CHAT"
- "Navajo"
- "PRC"
- "PST8PDT"
- "Pacific/Apia"
- "Pacific/Auckland"
- "Pacific/Bougainville"
- "Pacific/Chatham"
- "Pacific/Chuuk"
- "Pacific/Easter"
- "Pacific/Efate"
- "Pacific/Enderbury"
- "Pacific/Fakaofo"
- "Pacific/Fiji"
- "Pacific/Funafuti"
- "Pacific/Galapagos"
- "Pacific/Gambier"
- "Pacific/Guadalcanal"
- "Pacific/Guam"
- "Pacific/Honolulu"
- "Pacific/Johnston"
- "Pacific/Kiritimati"
- "Pacific/Kosrae"
- "Pacific/Kwajalein"
- "Pacific/Majuro"
- "Pacific/Marquesas"
- "Pacific/Midway"
- "Pacific/Nauru"
- "Pacific/Niue"
- "Pacific/Norfolk"
- "Pacific/Noumea"
- "Pacific/Pago_Pago"
- "Pacific/Palau"
- "Pacific/Pitcairn"
- "Pacific/Pohnpei"
- "Pacific/Ponape"
- "Pacific/Port_Moresby"
- "Pacific/Rarotonga"
- "Pacific/Saipan"
- "Pacific/Samoa"
- "Pacific/Tahiti"
- "Pacific/Tarawa"
- "Pacific/Tongatapu"
- "Pacific/Truk"
- "Pacific/Wake"
- "Pacific/Wallis"
- "Pacific/Yap"
- "Poland"
- "Portugal"
- "ROC"
- "ROK"
- "Singapore"
- "Turkey"
- "UCT"
- "US/Alaska"
- "US/Aleutian"
- "US/Arizona"
- "US/Central"
- "US/East-Indiana"
- "US/Eastern"
- "US/Hawaii"
- "US/Indiana-Starke"
- "US/Michigan"
- "US/Mountain"
- "US/Pacific"
- "US/Pacific-New"
- "US/Samoa"
- "UTC"
- "Universal"
- "W-SU"
- "WET"
- "Zulu"

## Environment variables

<a name="environment-variables"></a>

1. `API_KEY` - \*Deprecated

   - Creation: To get an `API_KEY` you will need an account. You can either use your existing account or create a Developer Account.

     - Existing account: You can create the key under your Account Settings.
     - Developer account: You will have to verify your email address first to create your Developer Account. Expect to get an email with a shortcut to create the `API_KEY`. Click on the shortcut link to create your `API_KEY` and get started writing some code.
