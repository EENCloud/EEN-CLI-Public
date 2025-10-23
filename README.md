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
  Enable detailed debug output.
- `-h, --help`
  Shows how to execute the selected subcommand and provides usage examples.
- `--prompt`
  Show user confirmation prompts.
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

The **een auth** command provides utilities for logging in and out of Eagle Eye Networks. When using `auth login`, the user is redirected to a login URL and completes the authentication in the web browser. However, when the `--v1` option is used, the users are authenticated directly through the CLI.

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

Log out from EEN.

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
een user list [options] [general options]
```

#### Options:

- `--csv`
  Export all users in CSV format.
- `-f, --file-name [file name]`
  Specify the file name to save the output under. Use with the `--csv` option to generate a report.
- `-g, --google-sheet`
  Export users in CSV format and upload to Google Sheets.
- `--header`
  Display column headers in the result.
- `--html`
  Generate an HTML report for user permissions.
- `--include [value1, value2]`
  Display associated items. supported values: email, firstname, id, lastname, permission, status.
- `-l, --long`
  Display user details, including name, email, last login, status, and permissions.
- `--v1`
  Use v1 APIs for listing users.

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

List all logged in accounts.

#### Usage:

```
een account list [options] [general options]
```

#### Options:

- `--csv`
  List all audit log in CSV format.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. supported values: id, name.
- `-l, --long`
  Display account details, including account ID, account name, and account type.
- `-s, --sub-account`
  List sub-accounts (only applicable for reseller accounts).

---

### switch

Switch to an account.

#### Usage:

```
een switch list [options] [general options]
```

#### Options:

- `-a, --account-id [account ID]`  
  Specify the Account ID to switch between logged-in accounts.
- `-s, --sub-account-id [sub-account ID]`  
  Specify the Sub Account ID to switch to from the reseller account.
- `--username [username]`  
  Specify the username to switch between logged-in accounts.

## EXAMPLES

- To list all accounts of the reseller:

```bash
een account list --header
```

#### Output

"account"
"Sijin Jacob(00052029)"
"Deepak M K(00064711)"

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
  Export the archive list in CSV format.
- `-D, --detailed`
  Retrieve a detailed list of archives with additional metadata.
- `--header`
  Display column headers in the result.
- `-l, --long`
  Display archive details, including filename, size, creation date, shared status, and shared path.
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
  The name of the archive to download (required).

#### Required Options:

- `-t, --target-directory [target-directory]`
  Specify the name of the directory where the output will be saved.

#### Optional Options:

- `-o, --overwrite`
  Overwrite the already downloaded archive if it exists.

## EXAMPLES

- To list available archives:

```bash
een archive list --detailed --csv --target-directory /path/to/output
```

- To download a specific archive:

```bash
een archive download <archive> --target-directory /path/to/save --overwrite --debug
```

# auditlog - Manage Audit logs

## NAME

`auditlog` - manage audit log.

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
  List all audit log in CSV format.
- `-e, --end-time [end time]`
  End time for audit log events(defaults to current time)
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List all audit log in CSV format in Google Sheets.
- `--header`
  Display column headers in the result. By default headers will be hidden.
- `-s, --start-time [start time]`
  Start time for audit log events(defaults to 10 minutes before the current time)

#### Selectors:

- `-u, --userid [user id]`
  Filter audit log by user-id.

## EXAMPLES

- To list all audit logs:

```bash
een auditlog list --header --csv
```

#### Output

```csv
"user","type","timestamp","description"
"Lakshmi Sai P(lpaspuleti+vs@een.com)","Create File","2025-10-07T09:43:17.851+00:00","File name "VSP Events Count Summary Report - 20251007094316035.html" created"
"Lakshmi Sai P(lpaspuleti+vs@een.com)","Create File","2025-10-07T09:43:17.461+00:00","File name "VSP Events Count Summary Report - 20251007094316035.csv" created"
```

- To list all audit logs for a specific time:

```bash
een auditlog list -s 20250328010101.000 -e 20250328010204.201
```

# availabledevices - Manage Available Devices

## NAME

`availabledevices` - manage available devices.

## SYNOPSIS

```
een availabledevices [COMMAND] [OPTIONS]
```

## COMMANDS

### list

List available devices.

#### Usage:

```
een availabledevices list [options] [general options]
```

#### Options:

- `--csv`
  List details in csv format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `-l, --long`
  Display user details, including make, model and IP Address.

#### Selectors:

- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter by bridge esn.
- `--devicestate [state1, state2]`
  Filter by device state. supported values: notSupported, addable, inOtherAccount, unknown.
- `--devicetype [type1, type2]`
  Filter by device types. supported values: camera, speaker, display, multiCamera.

## EXAMPLES

- To list all available devices:

```bash
een availabledevices list
```

- To list all available devices for a specific type:

```bash
een availabledevices list --devicetype 'camera, speaker' -d
```

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
  List all cameras, including shared ones.
- `--csv`
  List details in csv format.
- `--direct`
  List cameras which are direct to cloud.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `--html`
  Generate a chart in an html file.
- `--include [value1, value2]`
  Display associated items. supported values: esn, camera, bridge-esn, bridge, site, siteid, status, tag.
- `-l, --long`
  List camera details including camera, esn, bridge, bridge esn, site, site id, status, timezone, tags, shared, ip address and guid.
- `--shared`
  List cameras that are shared.
- `-T, --tree`
  List cameras and associated bridges in tree format.
- `--v1`
  Use v1 APIs.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `--site [site name1, site name2]`
  Filter based on site names.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
- `--status [status]`
  Filter based on status.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

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
een camera get [parameter] [value] [options] [selectors] [general options]
```

#### Parameters:

- `audio`
  Get audio settings(Is audio enabled or not).
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
  Get the preview video transmit mode.
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
  Export the result in CSV format.
- `--file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Export the result to Google Sheets.
- `--header`
  Display column headers in the result.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--esn [esn1, esn2]`
  Filter based on camera ESNs.
- `--site [site name1, site name2]`
  Filter based on site names.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
  `--status [status]`
  Filter based on status.
- `--tag [tag1, tag2]`
  Filter based on tags.

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
  Export the result in CSV format.
- `--file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  Export the result to Google Sheets.
- `--header`
  Display column headers in the result.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--esn [esn1, esn2]`
  Comma-separated list of camera ESNs to update, or use `'*'` to apply to all cameras.
- `--site [site name1, site name2]`
  Filter based on site names.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
  `--status [status]`
  Filter based on status.
- `--tag [tag1, tag2]`
  Filter based on tags.

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
  ESN of the camera (required)

---

### add

Add camera to bridge.

#### Usage:

```
een camera add <esn> [options] [general options]
```

#### Argument:

- `<esn>`
  ESN of the bridge to which the camera is added.

#### Required Options:

- `-C, --camera-name [camera name]`
  Name of the camera.
- `--guid [guid]`
  GUID of the camera.

#### Optional Options:

- `-c, --cloud-retention-days [cloud retention days]`
  Cloud retention days.
- `-p, --password [password]`
  Camera password.
- `-s, --scene [scene]`
  Scene.
- `-S, --site [site]`
  Site ID.
- `-t, --tag [tag1, tag2]`
  Tags.
- `-u, --username [username]`
  Camera username.

---

### streamstatus

Get camera stream status.

#### Usage:

```
een camera streamstatus [options] [general options]
```

#### Required Options:

- `-e, --end-time [end time]`
  Camera stream end time.
- `-s, --start-time [start time]`
  Camera stream start time.

#### Optional Options:

- `--esn [esn1, esn2]`
  ESNs of the cameras.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-S, --stream-type [stream type]`
  Stream type of the camera.

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
  List the camera purge list in csv format
- `-e, --end-time [end time]`
  Purge end time.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List the camera purge list in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.
- `-l, --long`
  List the camera purge list in long format.
- `-s, --start-time [start time]`
  Purge start time.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--esn [esn1, esn2]`
  Filter based on camera ESNs.
- `--site [site name1, site name2]`
  Filter based on site names.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
- `--status [status]`
  Filter based on status.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

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
  List the details in csv format
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List the details in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.
- `-l, --long`
  List the installer summary list in long format.

#### Selectors:

- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge esns.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.

---

### availability

Get camera availability.

#### Usage:

```
een camera availability [options] [selectors] [general options]
```

#### Required Options:

- `-s, --start-time [start time]`
  Video start time.

#### Optional Options:

- `--csv`
  List details in csv format.
- `-e, --end-time [end time]`
  End time for video.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `-N, --no-check`
  List all available data, including unchecked items.
- `-p, --preview-availability`
  Display preview recording status along with camera availability.
- `-s, --start-time [start time]`
  Start time for video (required).

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `--esn [esn1, esn2]`
  Filter based on camera ESNs.
- `--site [site name1, site name2]`
  Filter based on site names.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
- `--status [status]`
  Filter based on status.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

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
  List details in csv format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
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
  `--status [status]`
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

### deletetags

The `camera deletetag` command allows you to delete tags from camera.
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
  List details in csv format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
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
  `--status [status]`
  Filter by status.
- `--tag [tag1, tag2]`
  Filter by tags.

#### EXAMPLES

```bash
# delete tags newtag from camera with esns 1234,5678 give output in csv format with header:
een camera deletetag 'new tag' --esn '1234, 5678' --csv --header

# add tags test, new tag to camera with bridge esn 0987 and camera status online:
een camera addtag 'test, new tag' --bridge-esn '0987' --status 'online'
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
  List all bridges in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List bridges in CSV format in Google Sheets.
- `--header`
  Display column headers in the result.
- `--html`
  Generate a chart in HTML file.
- `--include[item 1, item 2]`
  display associated items. supported values: esn
- `-l, --long`
  Display bridge details including: "bridge id","bridge name","serial number","tags","connection status","timezone","site id","site name","mac address","guid","ip address","createtimestamp","number of cameras online","cloud bandwidth used last 7 days average","average available bandwidth last 7 days".
- `--v1`
  Use v1 APIs.

#### Selectors:

- `-s, --status [status]`
  Filter bridges with a specific status.
- `--site [site name1, site name2]`
  Filter bridges by site name.
- `--site-id [site id1, site id2]`
  Filter bridges by site id.
- `-t, --tag [tag1, tag2]`
  Filter bridges by tags.

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

Get bridge availability.

#### Usage:

```
een bridge availability [options] [selectors] [general options]
```

#### Required Options:

- `-s, --start-time [start time]`
  Specify video start time.

#### Optional Options:

- `--csv`
  List details in CSV format.
- `-e, --end-time [end time]`
  Specify video end time; ensure that the --start-time option is used.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `-N, --no-check`
  Show all available data.

#### Selectors:

- `--esn [esn1, esn2]`
  Filter bridges by bridge ESNs.
- `--site [site name1, site name2]`
  Filter bridges by sites.
- `--site-id [site id1, site id2]`
  Filter bridges by site IDs.
- `-t, --tag [tag1, tag2]`
  Filter bridges by tags.

---

### qlstreammetrics

Pull logs from the archiver/bridge.

#### Usage:

```
een  bridge qlstreammetrics [options] [general options]
```

#### Required Options:

- `--esn [esn1, esn2]`
  Esns of the bridge (required).

#### Optional Options:

- `-c, --count [count]`
  Specify the number of annotations to return.
- `-e, --end-time [end time]`
  Specify the end time.
- `-E, --events`
  View events of the bridge.
- `-l, --local-rtsp-metrics [enable/disable]`
  Enable or disable the RTSP metrics set.
- `-p, --performance`
  View performance metrics of the bridge.
- `-s, --start-time [start time]`
  Specify the start time.
- `-S, --summary`
  Get summarized data.

---

## EXAMPLES

- To list all bridges:

```bash
een bridge list
```

- To check the status of a specific bridge:

```bash
een bridge status --html
```

- To get availability information for a bridge:

```bash
een bridge availability --esn [esn1, esn2] --start-time [start time] --end-time [end time]
```

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
een switch list [options] [general options]
```

#### Options:

- `--csv`
  List details in csv format.
- `-f, --file-name`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. supported values: id, bridge, status.
- `-l, --long`
  List switch details, including switch ID, bridge ESN, and status.

## EXAMPLES

- To list all switches:

```bash
een switch list --header --csv
```

#### Output

```csv
"switch name"
"DiversitySwitch"
"Aut_v3_Switch_Bridge1"
```

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

List sensors.

#### Usage:

```
een sensor list [options] [general options]
```

#### Options:

- `--csv`
  List all sensors in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List all sensors in CSV format in Google Sheets.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. supported values: batterylevel, bluetoothsignal, id, name, parentid, status, site, siteid.
- `-l, --long`
  List sensor details, including name, id, parentId, battery level, bluetooth strength, site name and status.

## EXAMPLES

- To list all sensors:

```bash
een sensor list
```

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
een speaker list [options] [general options]
```

List speakers.

#### Options:

- `--csv`
  List all speakers in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List all speakers in CSV format in Google Sheets.
- `--header`
  Display column headers in the result. By default headers will be hidden.
- `-l, --long`
  List more details of speaker.

## EXAMPLES

- To list all speakers:

```bash
een speaker list
```

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
een site list [command] [options]
```

#### Options:

- `--csv`
  List all sites in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. supported values: siteid.
- `-l, --long`
  List site details, including site name and site ID.
- `-s, --site-id`
  List the IDs of the sites.

#### Actions:

- List sites with options for CSV format, file output, prompts, and debug output as specified.

## EXAMPLES

- To list all sites in CSV format:

```bash
een site list --csv --header
```

#### Output

```csv
"site name"
"Eagle Eye Bangalore"
"Eagle Eye India 1"
"Lakshmi test site 595"
```

- To get sites list in a file with prompting for confirmation:

```bash
een site list --csv --file-name sites.csv --prompt --debug
```

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
  List details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`
  Display associated items. Supported values: id, name, dfilename.
- `-l, --long`
  Display video details including id, name, dfilename, length, start-time and end-time.

###### Selectors:

- `-C, --camera [camera]`
  Filter based on camera name.
- `--esn [esn]`
  Filter based on camera ESN.

---

##### video export

Export video.

#### Usage:

```
een download video export [command] [options]
```

###### Options:

- `-C, --camera [camera]`
  Camera name.
- `-e, --end-time [end time]`
  End time.
- `--esn [esn]`
  Camera ESN.
- `--length [length]`
  Length from start time in seconds.
- `--name [name]`
  Export file name.
- `-s, --start-time [start time]`
  Start time (required).
- `-T, --timezone [timezone]`
  Timezone for timestamp (defaults to camera's timezone).
- `--timestamp`
  Add timestamp.
- `--max-length [max length] `
  Maximum duration in seconds for time-lapse video.
- `--time-lapse`
  Export a time-lapsed video.

---

##### video get

Download video.

#### Usage:

```
een download video get [options] [general options]
```

###### Options:

- `--dfilename [dfilename]`
  Filename to download.
- `--directory [directory]`
  Output directory.
- `-f, --file-name [file-name]`
  Override output file name.
- `--id [id]`
  ID of video to be downloaded.
- `--name [name]`
  Name of video to be downloaded.

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
een download preview [options] [general options]
```

#### Options:

- `-C, --camera [camera]`
  Camera to download from.
- `--directory [directory]`
  Output directory.
- `-e, --end-time [end time]`
  End time.
- `--esn [esn]`
  ESN to download from.
- `--length [length]`
  Length from start time in seconds.
- `--overlay`
  Add overlay.
- `-s, --start-time [start time]`
  Start time (required).
- `-T, --timezone [timezone]`
  Timezone for timestamp (default: camera's timezone).

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

- To delete a video by ID:

```bash
een download video delete video123
```

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
  List details in CSV format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `--jobid [job-id]`
  Filter by job ID.
- `--jobstate [state]`
  Filter by job state (pending, started, failure, success, revoked).

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

# video - Manage Recorded Videos

## NAME

`video` - manage and interact with recorded videos.

## SYNOPSIS

```
een video [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `video` command allows you to download recorded videos, list available videos, and check the status of preview recordings.

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

- `--esn [esn]`  
  ESNs of the camera.
- `-s, --start-time [start time]`  
  Video start time.

#### Optional Options:

- `--csv`  
  List preview recording status result in csv format.
- `-e, --end-time [end time]`  
  Video end time.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List camera recording status in CSV format in Google Sheets.
- `--header`  
  Display column headers in the result.

#### Actions:

- If ESNs and start time are provided, it checks the preview recording status. If the `--google-sheet` option is provided, the statuses will be listed in Google Sheets.

## EXAMPLES

- To download a video from a camera:

```bash
een video download --esn 123456 --start-time "20241001000000.000" --end-time "20241001010000.000" --format mp4 --target-directory /path/to/save
```

- To check the status of a preview recording:

```bash
een video previewrecordingstatus --esn 1005f355 --start-time  2024-11-17T09:20:54.619+00:00 --end-time  2024-11-18T09:20:54.619+00:00 --debug
```

# lpr - Manage License Plate Recognition (LPR) Events

## NAME

`lpr` - manage and retrieve License Plate Recognition events.

## SYNOPSIS

```
een lpr events [OPTIONS]
```

## DESCRIPTION

The `lpr events` command allows you to retrieve LPR events within a specified time frame. It supports filtering by license plate number and camera ESN.

## COMMANDS

### events

Get LPR events.

#### Usage:

```
een lpr events [options] [selectors] [general options]
```

#### Required Options:

- `-e, --end-time [end time]`
  Events end time.
- `-s, --start-time [start time]`
  Events start time.

#### Optional Options:

- `--header`
  Display column headers in the result.
- `--time`
  Display the execution time of the command.
- `--v1`
  Use v1 APIs.

#### Selectors:

- `--esn [esn1, esn2]`
  Filter by camera ESNs.
- `--layout [layout name1, layout name2]`
  Filter by Layout names associated with the camera.
- `--layout-id [layout id1, layout id2]`
  Filter by Layout IDs associated with the camera.
- `--lp [license plate]`
  Filter by License plate number.
- `-t, --tag [tag1, tag2]`
  Filter by camera tags.

#### Actions:

- If `--v1` is specified along with both `--start-time` and `--end-time`, it retrieves LPR events using v1 APIs.
- If only the start and end times are specified, it retrieves LPR events using the default API.

## EXAMPLES

- To get LPR events for a specific time frame:

```bash
een lpr events --start-time "20241001000000.000" --end-time "20241001010000.000"
```

- To get LPR events for a specific license plate:

```bash
een lpr events --start-time "20241001000000.000" --end-time "20241001010000.000" --lp "ABC123"
```

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
  List details in csv format.
- `-e, --end-time [end time]`
  LPR end time.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List VSP events in CSV format in Google Sheet.
- `--header`
  Display column headers in the result
- `--html`
  Generate chart in HTML file.
- `-s, --start-time [start time]`
  LPR start time.

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
  List details in csv format
- `-e, --end-time [end time]`
  LPR end time.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List VSP alerts in CSV format in Google Sheet
- `--header`
  Display column headers in the result
- `--html`
  Generate chart in HTML file.
- `-s, --start-time [start time]`
  LPR start time.

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

### vehiclelist

List all vehicle list

#### Usage:

```
een vsp list vehiclelist [options] [selectors] [general options]
```

#### Options:

- `--csv`
  List details in csv format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List VSP list vehiclelist in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.
- `--include [value1, value2]`  
  Display associated items. Supported values: id, name.
- `-l, --long`
  List more details of alerts.

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
  Filter by vehicle list name.
- `--plate [plate]`
  Filter by license plate number
- `--site [site name1, site name2]`
  Filter by site names.
- `--site-id [site id1, site id2]`
  Filter by site IDs.
  `--status [status]`
  Filter by status.
- `--tag [tag1, tag2]`
  Filter by tags.

## EXAMPLES

- To get VSP list vehiclelist in csv format with header:

```bash
een vsp list vehiclelist --csv --header
```

#### Output

```csv
"id","name","status","vehicle count","camera count","site count"
"406cdb01-3383-44d9-8884-7de9eefd6106","Testtt558","active","","12",""
"2ae96131-707a-46b3-ac87-5bcb427e9141","Test1234","active","1","12",""
"9ac3a7a6-040c-4e17-8f1f-632da3c1b0fc","Test0933","active","","12",""
```

- To get VSP list vehiclelist for esn '1234' with vehicle list name 'my name' in csv format with headers as long list:

```bash
een vsp list vehiclelist --csv --header -l --esn '1006b36f' --name 'EEN India North'
```

#### Output

```csv
"id","name","status","vehicle count","camera count","site count","camera name","site name","notes"
"416d8e21-a6f0-4b02-93a7-07cd01a9effa","EEN India North","active","19","1","2","108 Test camera (RMA ROOM)","Eagle Eye Bangalor,Eagle Eye India 1","EEN India office North road side facing camera"
```

---

### vehicle

List details of vehicle

#### Usage:

```
een vsp list vehicle [options] [selectors] [general options]
```

#### Options:

- `--csv`
  List details in csv format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List VSP list vehiclelist in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.
- `--id [id]`
  Display details of vehicles with the specified vehicle list id.
- `--include [value1, value2]`  
  Display associated items. Supported values: id, plate.
- `-l, --long`
  Display details of vehicles, including vehicle id, color, make, model, user tags, security status, vehicle list id.
- `--name [name]`
  Display details of vehicles with the specified vehicle list name.

#### Selectors:

- `--access-type [type1, type2]`
  Filter by access type.
- `--plate [plate]`
  Filter by license plate number.
- `--security-status [status1, status2]`
  Filter by security status.
- `--user-tag [tag1, tag2]`
  Filter by user tags.

## EXAMPLES

- To get VSP list vehicles with vehicle list name 'Hotlist Vehicles' in csv format with header:

```bash
een vsp list vehicle --name 'Hotlist Vehicles' --csv --header
```

#### Output

```csv
"license plate","accsss type","valid from","valid to","user data","vehicle list name"
"LHS7593","allow","","","","Hotlist Vehicles"
"SMY5299","allow","","","","Hotlist Vehicles"
"GZJ8668","allow","","","","Hotlist Vehicles"
```

- To get VSP list vehicles with vehicle list id '23j2j5' and user tags 'brivo' in csv format with headers as long list:

```bash
een vsp list vehicle --id 'e705d1f9-4846-4c98-aa09-20b5e54b694f' -l --header  --user-tags 'brivo' --csv
```

#### Output

```csv
"license plate","accsss type","valid from","valid to","user data","vehicle list name","id","color","make","model","user tags","security status","vehicle list id"
"VPM1767","allow","","","emp_id/1028, company/brivo","Employee List","ff149647-7146-4dd1-ba6a-a55640f53f29","","","","emp_id,1028,company,brivo","exempted","e705d1f9-4846-4c98-aa09-20b5e54b694f"
"TKN9576","allow","","","emp_id/1007, company/brivo","Employee List","fc540121-cb52-4fd9-b9ce-bc3abd43a7e1","","","","emp_id,1007,company,brivo","exempted","e705d1f9-4846-4c98-aa09-20b5e54b694f"
```

- To get VSP list vehicles with vehicle list name 'hotlist' and license plate number 'NJIFUI7' in csv format with headers as long list:

```bash
een vsp list vehicle --name 'Hotlist Vehicles'  -l --header  --plate 'PSM1356' --csv
```

#### Output

```csv
"license plate","accsss type","valid from","valid to","user data","vehicle list name","id","color","make","model","user tags","security status","vehicle list id"
"PSM1356","allow","","","","Hotlist Vehicles","f34478ea-46f5-4423-b5a0-23bbe5ad19f0","","","","","","3539f639-00d1-4c6b-b1a7-c66954f4cb93"
```

---

# pos - Manage Point of Sale (POS) Events

## NAME

`pos` - manage and retrieve Point of Sale events.

## SYNOPSIS

```
een pos listevents [OPTIONS]
```

## DESCRIPTION

The `pos` command allows you to manage and retrieve POS events based on parameters such as time, transaction details, and site.

## COMMANDS

### listevents

Get POS events.

#### Usage:

```
een pos listevents [options] [selectors] [general options]
```

#### Options:

- `--csv`
  List details in csv format
- `-e, --end-time [end time]`
  Defines the end point for retrieving events. The timestamp must be in ISO 8601 format with millisecond precision (e.g., YYYY-MM-DDTHH:MM:SS.sss±HH:MM).
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List POS events in CSV format in Google Sheet
- `--header`
  Display column headers in the result
- `--html`
  Generate chart in HTML file.
- `-s, --start-time [start time]`
  Defines the starting point for retrieving events. The timestamp must be in ISO 8601 format with millisecond precision (e.g., YYYY-MM-DDTHH:MM:SS.sss±HH:MM).

#### Selectors:

- `-b, --bill-number [bill number]`
  Filter by bill number.
- `--discount-max [discount max]`
  Filter by maximum discount percentage.
- `--discount-min [discount min]`
  Filter by minimum discount percentage.
- `-E, --employee-id [employee ID]`
  Filter by employee ID.
- `-F, --flagged`
  Filter by flagged transactions.
- `--net-amount-max [net amount max]`
  Filter by maximum net amount.
- `--net-amount-min [net amount min]`
  Filter by minimum net amount.
- `--site [site name1, site name2]`
  Filter by site names. Provide a comma-separated list of site names.
  `--site-id [site id1, site id2]`
  Filter by site IDs. Provide a comma-separated list of site IDs.
- `-t, --transaction-type [transaction type]`
  Filter by transaction type.

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

# perftest - Execute Performance Tests

## NAME

`perftest` - execute performance tests.

## SYNOPSIS

```
een perftest preview [OPTIONS]
```

## DESCRIPTION

The `perftest` command allows you to execute performance tests on various aspects of the platform.

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

## COMMANDS

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
  Number of previews to be tested (default: 10).
- `--csv`
  List details in csv format.
- `-e, --end-time [end time]`
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `--fixed`
  Generate timestamps at fixed intervals (interval: 10000 ms).
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `-s, --start-time [start time]`
  Specify the start timestamp for analysis.
- `--v1`
  Test performance of the V1 API.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--esn [esn1, esn2]`
  Filter based on camera ESNs.
- `--layout [layout1, layout2]`
  Filter based on layouts.
- `--layout-id [layout id1, layout id2]`
  Filter based on layouts IDs.
- `--site [site1, site2]`
  Filter based on sites.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

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
  Number of assets per list (default: 10).
- `--archiver`
  Display the archiver ID.
- `-c, --count [count]`
  Number of asset lists to be tested (default: 10).
- `--csv`
  List details in csv format.
- `-e, --end-time [end time]`
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `--fixed`
  Generate timestamps at fixed intervals (interval: 10000 ms).
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `-H, --headerinfo`
  Display response header info.
- `--header`
  Display column headers in the result.
- `-s, --start-time [start time]`
  Specify the start timestamp for analysis.

#### Selectors:

- `--bridge [bridge1, bridge2]`
  Test based on bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Test based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Test based on cameras.
- `--esn [esn1, esn2]`
  Test based on camera ESNs.
- `--layout [layout1, layout2]`
  Test based on layouts.
- `--layout-id [layout id1, layout id2]`
  Test based on layouts IDs.
- `--site [site1, site2]`
  Test based on sites.
- `--site-id [site id1, site id2]`
  Test based on site IDs.
- `-t, --tag [tag1, tag2]`
  Test based on tags.

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
  Number of pngspans to be tested (default: 10).
- `--csv`
  List details in csv format.
- `-e, --end-time [end time]`
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `--fixed`
  Generate timestamps at fixed intervals (interval: 10000 ms).
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `-H, --headerinfo`
  Display response header info.
- `--header`
  Display column headers in the result.
- `-s, --start-time [start time]`
  Specify the start timestamp for analysis.
- `--width [width]`
  Width of pngspan to be tested (default: 240).

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--esn [esn1, esn2]`
  Filter based on camera ESNs.
- `--layout [layout1, layout2]`
  Filter based on layouts.
- `--layout-id [layout id1, layout id2]`
  Filter based on layouts IDs.
- `--site [site1, site2]`
  Filter based on sites.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

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
  Number of videos to be tested (default: 10).
- `--csv`
  List details in csv format.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `-l, --length [length]`
  Specify the video duration for analysis (default: 5s).

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--esn [esn1, esn2]`
  Filter based on camera ESNs.
- `--layout [layout1, layout2]`
  Filter based on layouts
- `--layout-id [layout id1, layout id2]`
  Filter based on layout IDs.
- `--site [site1, site2]`
  Filter based on sites.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

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
  Number of videos frames to be tested (default: 10).
- `--csv`
  List details in csv format.
- `-f, --file-name [file name]`
  Specify the file name to save the test results.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--esn [esn1, esn2]`
  Filter based on camera ESNs.
- `--layout [layout1, layout2]`
  Filter based on layouts.
- `--layout-id [layout id1, layout id2]`
  Filter based on layouts IDs.
- `--site [site1, site2]`
  Filter based on sites.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

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
  Number of videos to be tested (default: 10).
- `--csv`
  List details in csv format.
- `-e, --end-time [end time]`
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `--fixed`
  Generate timestamps at fixed intervals.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `-l, --length [video length]`
  Specify the video duration for analysis (default: 10s).
- `-s, --start-time [start time]`
  Specify the start timestamp for analysis.

#### Selectors:

- `-b, --bridge [bridge1, bridge2]`
  Filter based on bridge names.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Filter based on bridge ESNs.
- `-C, --camera [camera1, camera2]`
  Filter based on camera names.
- `--esn [esn1, esn2]`
  Filter based on camera ESNs.
- `--layout [layout1, layout2]`
  Filter based on layouts.
- `--layout-id [layout id1, layout id2]`
  Filter based on layouts IDs.
- `--site [site1, site2]`
  Filter based on sites.
- `--site-id [site id1, site id2]`
  Filter based on site IDs.
- `-t, --tag [tag1, tag2]`
  Filter based on tags.

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
