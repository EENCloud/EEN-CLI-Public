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
  ./een --version
  ```

- To check if the executable works fine

  - Run the command:

  ```
   ./een
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

The **een auth** command provides utilities for logging in and out of Eagle Eye Networks.

## COMMANDS

### login

Log in to EEN using the provided credentials.

#### Required options:

- `-p, --password <password>`  
  Password for login. Use quotes around the password if it contains special characters (e.g., `--password "MyP@ssw0rd!"`).

- `-u, --username <username>`  
  Username for login (e.g., `--username admin@example.com`).

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--time`  
  Display the execution time of the command.

#### Notes:

- If the shell misinterprets special characters, ensure the password is wrapped in quotes.

---

### logout

Log out from EEN.

#### Options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--time`  
  Display the execution time of the command.

## EXAMPLES

- To login

```bash
een auth login --username johndoe --password secret --debug
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

#### Options:

- `--call-time`  
  Get api response time.
- `--csv`  
  Export all users in CSV format.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --email`  
  Display user email addresses.
- `-f, --file-name [file name]`  
  Specify the file name to save the output under. Use with the `--csv` option to generate a report.
- `-F, --first-name`  
  Display user first names.
- `-g, --google-sheet`  
  Export users in CSV format and upload to Google Sheets.
- `--header`  
  Display column headers in the result.
- `--html`  
  Generate an HTML report for user permissions.
- `-l, --long`  
  Display user details, including name, email, last login, status, and permissions.
- `-L, --last-name`  
  Display user last names.
- `-p, --permission`  
  Display user permissions.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --status`  
  Display user statuses.
- `--time`  
  Display the execution time of the command.
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
een user list
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

#### Options:

- `-a, --account-id`  
  List account ID.
- `-A, --account-name`  
  List account name.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--header`  
  Display column headers in the result.
- `-l, --long`  
  Display account details, including account ID, account name, and account type.
- `-s, --sub-account`  
  List sub-accounts (only applicable for reseller accounts).
- `--time`  
  Display the execution time of the command.

---

### switch

Switch to an account.

#### Options:

- `-a, --account-id [account ID]`  
  Specify the Account ID to switch between logged-in accounts.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-s, --sub-account-id [sub-account ID]`  
  Specify the Sub Account ID to switch to from the reseller account.
- `--time`  
  Display the execution time of the command.
- `--username [username]`  
  Specify the username to switch between logged-in accounts.

## EXAMPLES

- To list all accounts of the reseller:

```bash
een account list --debug
```

- To switch to a specific sub-account:

```bash
een account switch --sub-account-id <sub-account ID> --debug
```

- To switch to a specific account:

```bash
een account switch --account-id <account ID> --debug
```

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

#### Options:

- `--call-time`  
  Get api response time.
- `--csv`  
  Export the archive list in CSV format.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-D, --detailed`  
  Retrieve a detailed list of archives with additional metadata.
- `--header`  
  Display column headers in the result.
- `-l, --long`  
  Display archive details, including filename, size, creation date, shared status, and shared path.
- `-t, --target-directory [target directory]`  
  Specify the directory from which the archive will be retrieved.
- `--time`  
  Display the execution time of the command.

---

### download

Download a specific archive.

#### Arguments:

- `<archive>`  
  The name of the archive to download (required).

#### Required options:

- `-t, --target-directory [target-directory]`  
  Specify the name of the directory where the output will be saved.

#### Optional options:

- `--call-time`
  Get API response time.
- `-d, --debug`  
  Enable debug output for troubleshooting.
- `-o, --overwrite`  
  Overwrite the already downloaded archive if it exists.
- `--time`  
  Display the execution time of the command.

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

#### Options:

- `--call-time`
  Get api response time.
- `--csv`
  List all audit log in CSV format.
- `-d, --debug`
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`
  End time for audit log events(defaults to current time)
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List all audit log in CSV format in Google Sheets.
- `-H, --header`
  Display column headers in the result. By default headers will be hidden.
- `--prompt`
  Show user confirmation prompts.
- `-s, --start-time [start time]`
  Start time for audit log events(defaults to 10 minutes before the current time)
- `--time`
  Display the execution time of the command.
- `-u, --userid [user id]`
  Filter audit log by user-id

## EXAMPLES

- To list all audit logs:

```bash
een auditlog list
```

- To list all audit logs for a specific time:

```bash
een auditlog list -s 20250328010101.000 -e 20250328010204.201
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

#### Options:

- `-a, --available`  
  List available cameras that are currently operational.
- `-A, --all`  
  List all cameras without filtering.
- `-b, --bridge`  
  List bridge name of the cameras.
- `-B, --bridge-esn`  
  List bridge ESNs of the cameras.
- `-C, --camera`  
  List cameras.
- `--call-time`  
  Get API response time.
- `--csv`  
  List cameras in CSV format.
- `-d, --debug`  
  Enable debug output for troubleshooting and detailed logs.
- `--direct`  
  List cameras which are direct to cloud.
- `-e, --end-time [end time]`  
  Filter cameras based on video end time. Format: `YYYYMMDDHHMMSS.sss` (Compact ISO 8601 date-time with milliseconds).
- `--esn`  
  List cameras ESNs.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `filter-layout [layout name1, layout name2]`  
  Filter cameras by layout.
- `filter-layout-id [layout id, layout id]`  
  Filter cameras by layout ID.
- `filter-site [site name1, site name2]`
  Filter cameras by site.
- `filter-site-id [site id1, site id2]`
  Filter cameras by site ID.
- `filter-status <status>`
  Filter cameras by status
- `-g, --google-sheet`  
  List cameras in CSV format in a Google Sheet.
- `-H, --header`  
  Display column headers in the result.
- `--html`  
  Generate a chart of the camera list in an HTML file format.
- `-l, --long`  
  List camera details, including camera, camera ESN, bridge, bridge ESN, site, site ID, status, tags, shared, timezone, IP address and GUID.
- `--prompt`  
  Show user confirmation prompts during the command execution.
- `-s, --start-time [start time]`  
  Filter cameras based on video start time. Format: `YYYYMMDDHHMMSS.sss` (Compact ISO 8601 date-time with milliseconds).
- `--shared`  
  List cameras that are shared with other users.
- `--short`  
  List only the camera names and ESNs in CSV format to the specified file.
- `--site`  
  List sites of the cameras.
- `--site-id`  
  List site IDs of the cameras.
- `--status`  
  List status of the cameras.
- `-t, --tag [tag1, tag2]`  
  Filter cameras by tags.
- `-T, --tree`  
  List cameras and associated bridges in a tree format.
- `--tag`  
  List tags of the cameras.
- `--time`  
  Display the execution time of the command.
- `--v1`  
  Use version 1 APIs for backward compatibility.

#### Notes:

- Start-time and end-time must follow the format: `YYYYMMDDHHMMSS.sss` (Compact ISO 8601 date-time with milliseconds).

---

### status

List status of all cameras.

#### Options:

- `--call-time`  
  Get api response time.
- `--csv`  
  List camera status in CSV format.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List camera status in CSV format in Google Sheet.
- `--html`  
  Generate chart in HTML file.
- `--layout [layout name1, layout name2]`  
  Layout names associated with the camera.
- `--layout-id [layout id1, layout id2]`  
  Layout IDs associated with the camera.
- `--prompt`  
  Show user confirmation prompts.
- `-t, --tag [tag1, tag2]`  
  Filter cameras using tags.
- `--time`  
  Display the execution time of the command.
- `--v1`  
  Use v1 APIs.

---

### settings

Get all camera settings.

#### Required options:

- `--csv`  
  List camera settings.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-H, --header`  
  Display column headers in the result.
- `j, --json`
  List settings in JSON format
- `-l, --long`  
  List the camera settings in long format.
- `--prompt`  
  Show user confirmation prompts.
- `--time`  
  Display the execution time of the command.
- `--v1`
  Use v1 APIs

---

### set

Edit camera's settings.

#### Arguments:

- `-b, --bridge [bridge1, bridge2]`  
  Edit camera settings by bridge ESNs.
- `--esn [esn1, esn2]`  
  Edit camera settings by camera ESNs.
- `-f, --file-name [file name]`  
  Edit camera settings by reading the CSV file.
- `-T, --tag [tag1, tag2]`  
  Edit camera settings by tag.
- `-s, --site-id [site id1, site id2]`  
  Edit camera settings by site id.
- `-S, --site [site name1, site name2]`  
  Edit camera settings by site name.
- `--layout-id [layout id1, layout id2]`  
  Edit camera settings by layout id.
- `--layout [layout name1, layout name2]`  
  Edit camera settings by layout name.
- `--prompt`  
  Show user confirmation prompts.

#### Options:

- `-a, --aspect-ratio [aspect ratio]`  
  Preview aspect ratio.
- `--audio-disable`  
  Disable audio.
- `--audio-enable`  
  Enable audio.
- `-B, --bridge-target-days [bridge target days]`  
  Bridge target days.
- `-c, --cloud-retention-days [cloud retention days]`  
  Cloud retention days.
- `-C, --camera-name [camera name]`  
  Camera name.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-L, --local-retention-days [local retention days]`  
  Local retention days.
- `--layout [layout name1, layout name2]`  
  Layout names associated with the camera.
- `--layout-id [layout id1, layout id2]`  
  Layout IDs associated with the camera.
- `-p, --password [password]`  
  Password.
- `--preview-interval-ms [preview interval ms]`  
  Preview interval rate in milliseconds.
- `--preview-only-cloud-retention [preview only cloud retention]`  
  Preview only cloud retention.
- `--preview-quality [preview quality]`  
  Preview quality.
- `--preview-resolution [preview resolution]`  
  Preview resolution.
- `--preview-transmit-mode [preview transmit mode]`  
  Preview transmit mode.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --site-id [site id1, site id2]`  
  Site IDs associated with the camera.
- `-S, --site [site name1, site name2]`  
  Site name associated with the camera.
- `-t, --tag [tag1, tag2]`  
  Tags associated with camera.
- `--time`  
  Display the execution time of the command.
- `-u, --username [username]`  
  Username.
- `--video-capture-mode [video capture mode]`  
  When to record video.
- `--video-quality [video quality]`  
  Video quality.
- `--video-resolution [video resolution]`  
  Video resolution.
- `--video-transmit-mode [video transmit mode]`  
  Video transmit mode.

---

#### Notes:

- For `--esn "*"`, it changes settings for all cameras.

### delete

Delete a camera from the bridge.

#### Argument:

- `<esn>`  
  ESN of the camera (required)

#### Options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--prompt`  
  Show user confirmation prompts.
- `--time`  
  Display the execution time of the command.

---

### add

Add camera to bridge.

#### Argument:

- `<esn>`  
  ESN of the bridge to which the camera is added.

#### Required options:

- `-C, --camera-name [camera name]`  
  Name of the camera.
- `--guid [guid]`  
  GUID of the camera.

#### Optional options:

- `-c, --cloud-retention-days [cloud retention days]`  
  Cloud retention days.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-p, --password [password]`  
  Camera password.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --scene [scene]`  
  Scene.
- `-S, --site [site]`  
  Site ID.
- `-t, --tag [tag1, tag2]`  
  Tags.
- `--time`  
  Display the execution time of the command.
- `-u, --username [username]`  
  Camera username.

---

### streamstatus

Get camera stream status.

#### Required options:

- `-e, --end-time [end time]`  
  Camera stream end time.
- `-s, --start-time [start time]`  
  Camera stream start time.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--esn [esn1, esn2]`  
  ESNs of the cameras.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--prompt`  
  Show user confirmation prompts.
- `-S, --stream-type [stream type]`  
  Stream type of the camera.
- `--time`  
  Display the execution time of the command.

#### Notes:

- `stream-type` can be **"fullvideo"** or **"preview"**.
- `start-time` can be **"-1h"** (one hour before current time).
- `end-time` can be **"now"** (current time).

---

### purgelist

Get camera purging and duty cycle.

#### Options:

- `--call-time`  
  Get api response time.
- `--csv`
  List the camera purge list in csv format
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
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
- `--prompt`  
  Show user confirmation prompts.
- `-s, --start-time [start time]`  
  Purge start time.
- `--time`  
  Display the execution time of the command.

#### Notes:

- If you haven't specified any start-time and end-time, it will take the last 24 hours as default timestamps.

---

### i-summary

Get camera installer summary.

#### Options:

- `--call-time`
  Get api response time.
- `--csv`
  List the details in csv format
- `-d, --debug`
  Enable detailed debug output for troubleshooting.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List the details in CSV format in Google Sheet.
- `--header`
  Display column headers in the result.
- `-l, --long`
  List the installer summary list in long format.
- `--prompt`
  Show user confirmation prompts.
- `--time`
  Display the execution time of the command.

---

### availability

Get camera availability.

#### Required options:

- `-s, --start-time [start time]`  
  Video start time.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Video end time.
- `--esn [esn1, esn2]`  
  ESNs of the camera.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List camera availability in CSV format in Google Sheets.
- `--layout [layout name1, layout name2]`
  Layout names associated with the camera.
- `--layout-id [layout id1, layout id2]`
  Layout IDs associated with the camera.
- `-N, --no-check`  
  Show all available data, including unchecked items.
- `-p, --preview-availability`  
  Get preview recording status along with camera availability.
- `--prompt`  
  Show user confirmation prompts.
- `--site [site name1, site name2]`  
  List cameras located in the specified sites. Provide a comma-separated list of site names.
- `--site-id [site id1, site id2]`  
  List cameras located in the specified sites. Provide a comma-separated list of site IDs.
- `-t, --tag [tag1, tag2]`  
  Filter cameras using tags.
- `--time`  
  Display the execution time of the command.

#### Notes:

- This command only supports a maximum of 200 devices and a seven-day time range.

---

### addtags

Add tags to camera, accepts multiple tags and esns seperated by comma

#### Argument:

- `<esns>`  
  ESNs of the cameras to which the tags are added.
- `<tags>`  
  Tags to be added to the cameras.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--time`  
  Display the execution time of the command.

---

### deletetags

Delete tags from camera, accepts multiple tags and esns seperated by comma

#### Argument:

- `<esns>`  
  ESNs of the cameras from which the tags are deleted.
- `<tags>`  
  Tags to be deleted from the cameras.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--time`  
  Display the execution time of the command.

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

#### Options:

- `-a, --available`  
  List discovered cameras that are not yet attached.
- `--call-time`  
  Get api response time.
- `--csv`  
  List all bridges in CSV format.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--esn`  
  List bridge ESNs.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List bridges in CSV format in Google Sheets.
- `--header`  
  Display column headers in the result.
- `--html`  
  Generate a chart in HTML file.
- `-l, --long`  
  Display bridge details, including bridge ID, name, and location. For v3, also includes cameras in the account and online cameras; for v1, includes GUID.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --status [status]`  
  List bridges with a specific status.
- `--site [site name1, site name2]`
  List bridges in a specific site name.
- `--site-id [site id1, site id2]`  
  List bridges in a specific site id.
- `-t, --tag [tag1, tag2]`  
  Filter bridges by tags.
- `-T, --tree`  
  View bridges and associated cameras in tree format.
- `--time`  
  Display the execution time of the command.
- `--v1`  
  Use v1 APIs.

#### Actions:

- If `--html` is specified and `--v1`, generate a bridge list report using v1.
- If `--csv` is specified and `--v1`, list bridges in CSV format using v1.
- Handle other combinations of options to perform various listing and reporting tasks.

---

### status

List bridge status.

#### Options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting
- `-g, --google-sheet`  
  List bridges in csv format in a Google Sheet
- `--html`  
  Generate a chart in an HTML file
- `--time`  
  Display the execution time of the command.

---

### availability

Get bridge availability.

#### Required options:

- `-s, --start-time [start time]`  
  Specify video start time.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`
  Specify video end time.
- `--esn [esn1, esn2]`  
  ESNs of the bridge
- `-f, --file-name [file name]`  
  Specify the file name to save the output
- `-g, --google-sheet`  
  List bridge availability in csv format in a Google Sheet
- `-N, --no-check`  
  Show all available data
- `--prompt`  
  Show user confirmation prompts
- `--site [site name1, site name2]`
  Site name associated with the bridge
- `--site-id [site id1, site id2]`  
  Site ID associated with the bridge.
- `-t, --tag [tag1, tag2]`  
  Filter bridges using tags.
- `--time`  
  Display the execution time of the command.

---

### qlstreammetrics

Pull logs from the archiver/bridge.

#### Required options:

- `--esn [esn1, esn2]`  
  Esns of the bridge (required).

#### Optional options:

- `-c, --count [count]`  
  Specify the number of annotations to return
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting
- `-e, --end-time [end time]`  
  Specify the end time
- `-E, --events`  
  View events of the bridge
- `-l, --local-rtsp-metrics [enable/disable]`  
  Enable or disable the RTSP metrics set
- `-p, --performance`  
  View performance metrics of the bridge
- `--prompt`  
  Show user confirmation prompts
- `-s, --start-time [start time]`  
  Specify the start time
- `-S, --summary`  
  Get summarized data
- `--time`  
  Display the execution time of the command.

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

#### Options:

- `-b, --bridge`
  List the bridge ESNs associated with the switches.
- `--call-time`
  Get api response time.
- `--csv`
  List details in csv format.
- `-d, --debug`
  Enable detailed debug output for troubleshooting.
- `-f, --file-name`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `--id`
  List the IDs of the switches.
- `-l, --long`
  List switch details, including switch ID, bridge ESN, and status.
- `--prompt`
  Show user confirmation prompts (default: false).
- `-s, --status`
  List the status of the switches.
- `--time`
  Display the execution time of the command.

## EXAMPLES

- To list all switches:

```bash
een switch list
```

- To list switches ids:

```bash
een switch list --id
```

- To list switches and their statuses:

```bash
een switch list --status
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

#### Options:

- `-b, --battery-level`
  List battery level of sensors.
- `B, --bt-signal`
  List bluetooth signal strength of the sensors.
- `--call-time`  
  Get api response time.
- `--csv`  
  List all sensors in CSV format.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List all sensors in CSV format in Google Sheets.
- `-H, --header`  
  Display column headers in the result.
- `--id`
  List ID of sensors.
- `-l, --long`  
  List sensor details, including name, id, parentId, battery level, bluetooth strength, site name and status.
- `--name`
  List name of sensors.
- `--parent-id`
  List parent id of sensors.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --status`
  List status of sensors.
- `--site`
  List site name of sensors.
- `--site-id`  
  List site ID of sensors.
- `--time`  
  Display the execution time of the command.

## EXAMPLES

- To list all sensors:

```bash
een sensor list
```

- To list sensor names:

```bash
een sensor list --name
```

- To list sensor names and their statuses:

```bash
een sensor list --name --status
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

List speakers.

#### Options:

- `--call-time`
  Get api response time.
- `--csv`
  List all speakers in CSV format.
- `-d, --debug`
  Enable detailed debug output for troubleshooting.
- `-f, --file-name [file name]`
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`
  List all speakers in CSV format in Google Sheets.
- `-H, --header`
  Display column headers in the result. By default headers will be hidden.
- `-l, --long`
  List more details of speaker.
- `--prompt`
  Show user confirmation prompts.
- `--time`
  Display the execution time of the command.

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

#### Options:

- `--call-time`  
  Get api response time.
- `--csv`  
  List all sites in CSV format.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--header`  
  Display column headers in the result.
- `-l, --long`  
  List site details, including site name and site ID.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --site-id`  
  List the IDs of the sites.
- `--time`  
  Display the execution time of the command.

#### Actions:

- List sites with options for CSV format, file output, prompts, and debug output as specified.

## EXAMPLES

- To list all sites in CSV format:

```bash
een site list --csv --file-name sites.csv
```

- To get sites list in a file with prompting for confirmation:

```bash
een site list --csv --file-name sites.csv --prompt --debug
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

## COMMANDS

### download

Download video from the camera.

#### Required options:

- `-e, --end-time [end time]`  
  Video end time.
- `--esn [esn]`  
  ESN of the camera.
- `-f, --format [format]`  
  Video format.
- `-s, --start-time [start time]`  
  Video start time.
- `-t, --target-directory [target-directory]`  
  Specify the directory where the video will be saved.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-o, --overwrite`  
  Overwrite the existing video file.
- `-T, --timezone [timezone]`  
  Timezone to use for the video download.
- `--time`  
  Display the execution time of the command.

#### Notes:

- Video downloads support both mp4 and FLV formats.
- The timezone option is only supported for mp4 format.
- Video downloading is done in batches of 5 videos at a time.

#### Actions:

- Downloads the video from the specified camera if all required options are provided.

---

### list

Get a list of videos from the selected camera.

#### Required options:

- `-e, --end-time [end time]`  
  Video end time.
- `--esn [esn]`  
  ESN of the camera.
- `-s, --start-time [start time]`  
  Video start time.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--header`
  Display column headers in the result.
- `--time`  
  Display the execution time of the command.

#### Actions:

- Lists videos available from the specified camera within the given time frame.

---

### previewrecordingstatus

Get the status of preview recording.

#### Required options:

- `--esn [esn]`  
  ESNs of the camera.
- `-s, --start-time [start time]`  
  Video start time.

#### Optional options:

- `--call-time`  
  Get api response time.
- `--csv`  
  List preview recording status result in csv format.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Video end time.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List camera recording status in CSV format in Google Sheets.
- `--header`  
  Display column headers in the result.
- `--prompt`  
  Show user confirmation prompts.
- `--time`  
  Display the execution time of the command.

#### Actions:

- If ESNs and start time are provided, it checks the preview recording status. If the `--google-sheet` option is provided, the statuses will be listed in Google Sheets.

## EXAMPLES

- To download a video from a camera:

```bash
een video download --esn 123456 --start-time "20241001000000.000" --end-time "20241001010000.000" --format mp4 --target-directory /path/to/save
```

- To list videos from a camera:

```bash
een video list --esn 123456 --start-time "20241001000000.000" --end-time "20241001010000.000" --debug
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

#### Required options:

- `-e, --end-time [end time]`  
  Events end time.
- `-s, --start-time [start time]`  
  Events start time.

#### Optional options:

- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--esn [esn1, esn2]`  
  The ESN for camera of interest.
- `--layout [layout name1, layout name2]`  
  Layout names associated with the camera.
- `--layout-id [layout id1, layout id2]`  
  Layout IDs associated with the camera.
- `--lp [license plate]`  
  License plate number.
- `-t, --tag [tag1, tag2]`  
  Filter by camera tags.
- `--time`
  Display the execution time of the command.
- `--v1`  
  Use v1 APIs.

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
een vsp [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `vsp` command allows you to manage and retrieve VSP events and alerts based on parameters such as time, vehicle characteristics, and alert types.

## COMMANDS

### listevents

Get VSP events.

#### Options:

- `-a, --access-type [access type]`  
  Access type.
- `-b, --body-type [types]`  
   Vehicle body types.
- `-c, --color [colors]`  
  Vehicle colors.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-D, --direction [directions]`  
  Direction of the vehicle.
- `-e, --end-time [end time]`  
  LPR end time.
- `--esn [esn1, esn2]`  
  Camera ESNs.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List VSP events in CSV format in Google Sheet
- `--html`  
  Generate chart in HTML file.
- `--lp [lp]`  
  License plate number.
- `-m, --make [makes]`  
  Vehicle makes.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --start-time [start time]`  
  LPR start time.
- `--site [site name1, site name2]`  
  List events in the specified sites. Provide a comma-separated list of site names.
- `--site-id [site id1, site id2]`  
  List events in the specified sites. Provide a comma-separated list of site IDs.
- `--time`  
  Display the execution time of the command.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.

#### Actions:

- If `--html` is specified, it generates a report of VSP events.
- If not, it retrieves VSP events and saves them according to the specified options.

---

### listalerts

Get VSP alerts.

#### Options

- `-a, --allowed-vehicle`  
  Alert type - allowed vehicle.
- `-c, --count-of-license-plate`  
  Alert type - count of license plate.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-D, --denied-vehicle`  
  Alert type - denied vehicle.
- `-e, --end-time [end time]`  
  LPR end time.
- `--esn [esn1, esn2]`  
  Camera ESN.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List VSP alerts in CSV format in Google Sheet
- `-H, --hotlist`  
  Alert type - hotlist.
- `--html`  
  Generate chart in HTML file.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --start-time [start time]`  
  LPR start time.
- `--site [site name1, site name2]`  
  List alerts in the specified sites. Provide a comma-separated list of site names.
- `--site-id [site id1, site id2]`  
   List alerts in the specified sites. Provide a comma-separated list of site IDs.
- `--time`  
  Display the execution time of the command.
- `-u, --unregistered-vehicle`  
  Alert type - unregistered vehicle.
- `-w, --watch-vehicle`  
  Alert type - watch vehicle.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.

#### Actions:

- If `--html` is specified, it generates a report of VSP alerts.
- If not, it retrieves VSP alerts and saves them according to the specified options.

## EXAMPLES

- To get VSP events for a specific time frame:

```bash
een vsp listevents --start-time "20241001000000.000" --end-time "20241001235959.000"
```

- To get VSP alerts for allowed vehicles:

```bash
een vsp listalerts --start-time 2024-11-17T09:20:54.619+00:00 --end-time 2024-11-18T09:20:54.619+00:00 --allowed-vehicle
```

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

#### Options

- `-b, --bill-number [bill number]`  
  Specify the bill number.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--discount-max [discount max]`  
  Specify the maximum discount in percentage.
- `--discount-min [discount min]`  
  Specify the minimum discount in percentage.
- `-e, --end-time [end time]`  
  Defines the end point for retrieving events. The timestamp must be in ISO 8601 format with millisecond precision (e.g., YYYY-MM-DDTHH:MM:SS.sss±HH:MM).
- `-E, --employee-id [employee ID]`  
  Specify the ID of the employee.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-F, --flagged`  
  Retrieve flagged transactions.
- `-g, --google-sheet`  
  List POS events in CSV format in Google Sheet
- `--html`  
  Generate chart in HTML file.
- `--net-amount-max [net amount max]`  
  Specify the maximum net amount.
- `--net-amount-min [net amount min]`  
  Specify the minimum net amount.
- `--prompt`  
  Show user confirmation prompts.
- `-s, --start-time [start time]`  
  Defines the starting point for retrieving events. The timestamp must be in ISO 8601 format with millisecond precision (e.g., YYYY-MM-DDTHH:MM:SS.sss±HH:MM).
- `--site [site name1, site name2]`  
  List events in the specified sites. Provide a comma-separated list of site names.
  `--site-id [site id1, site id2]`  
   List events in the specified sites. Provide a comma-separated list of site IDs.
- `-t, --transaction-type [transaction type]`  
  Specify the type of the transaction.
- `--time`  
  Display the execution time of the command.

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

## COMMANDS

### preview

Get performance test results for preview images.

#### Options

- `-a, --all-log`  
  Display execution logs.
- `--bridge [bridge1, bridge2]`  
  Test based on bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`  
  Test based on bridge ESNs.
- `-c, --count [count]`  
  Number of previews to be tested (default: 10).
- `-C, --camera [camera1, camera2]`  
   Test based on cameras.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `--esn [esn1, esn2]`  
  Test based on camera ESNs.
- `-f, --file-name [file name]`  
  Specify the file name to save the test results.
- `--header`  
  Display column headers in the result.
- `--layout [layout1, layout2]`  
  Test based on layouts.
- `--layout-id [layout id1, layout id2]`  
  Test based on layouts IDs.
- `-s, --start-time [start time]`  
  Specify the start timestamp for analysis.
- `--site [site1, site2]`  
  Test based on sites.
- `--site-id [site id1, site id2]`  
  Test based on site IDs.
- `-t, --table`  
  Display result in table format.
- `--tag [tag1, tag2]`  
  Test based on tags.
- `--time`  
  Display the execution time of the command.
- `--v1`  
  Test performance of the V1 API.

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

#### Options

- `-a, --all-log`  
  Display execution logs.
- `-A, --asset-count [asset count]`  
  Number of assets per list (default: 10).
- `--bridge [bridge1, bridge2]`  
  Test based on bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`  
  Test based on bridge ESNs.
- `-c, --count [count]`  
  Number of asset lists to be tested (default: 10).
- `-C, --camera [camera1, camera2]`  
  Test based on cameras.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `--esn [esn1, esn2]`  
  Test based on camera ESNs.
- `-f, --file-name [file name]`  
  Specify the file name to save the test results.
- `--header`  
  Display column headers in the result.
- `-H, --headerinfo`  
  Display response header info
- `--layout [layout1, layout2]`  
  Test based on layouts.
- `--layout-id [layout id1, layout id2]`  
  Test based on layouts IDs.
- `-s, --start-time [start time]`  
  Specify the start timestamp for analysis.
- `--site [site1, site2]`  
  Test based on sites.
- `--site-id [site id1, site id2]`  
  Test based on site IDs.
- `-t, --table`  
  Display result in table format.
- `--tag [tag1, tag2]`  
  Test based on tags.
- `--time`  
  Display the execution time of the command.

#### Notes:

- If no start time or end time is specified, the test interval will be last 30 days.

## EXAMPLES

- To test asset list performance of all the cameras in an account for last 30 days:

```bash
een perftest assetlist
```

- To test asset list performance of all the cameras in a specific layout:

```bash
een perftest assetlist --layout "layout1"
```

- To test asset list performance of all the cameras in a specific site:

```bash
een perftest assetlist --site "site1"
```

### pngspan

Get performance test results for pngspan endpoint.

#### Options

- `-a, --all-log`  
  Display execution logs.
- `--bridge [bridge1, bridge2]`  
  Test based on bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`  
  Test based on bridge ESNs.
- `-c, --count [count]`  
  Number of previews to be tested (default: 10).
- `-C, --camera [camera1, camera2]`  
  Test based on cameras.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `--esn [esn1, esn2]`  
  Test based on camera ESNs.
- `-f, --file-name [file name]`  
  Specify the file name to save the test results.
- `--header`  
  Display column headers in the result.
- `-H, --headerinfo`  
  Display response header info
- `--layout [layout1, layout2]`  
  Test based on layouts.
- `--layout-id [layout id1, layout id2]`  
  Test based on layouts IDs.
- `-s, --start-time [start time]`  
  Specify the start timestamp for analysis.
- `--site [site1, site2]`  
  Test based on sites.
- `--site-id [site id1, site id2]`  
  Test based on site IDs.
- `-t, --table`  
  Display result in table format.
- `--tag [tag1, tag2]`  
  Test based on tags.
- `--time`  
  Display the execution time of the command.
- `--width [width]`  
  Width of pngspan to be tested.

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

#### Options

- `-a, --all-log`  
  Display execution logs.
- `--bridge [bridge1, bridge2]`  
  Test based on bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`  
  Test based on bridge ESNs.
- `-c, --count [count]`  
  Number of videos to be tested (default: 1).
- `-C, --camera [camera1, camera2]`  
  Test based on cameras.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--esn [esn1, esn2]`  
  Test based on camera ESNs.
- `-f, --file-name [file name]`  
  Specify the file name to save the test results.
- `--header`  
  Display column headers in the result.
- `-l, --length`  
  Specify the video duration for analysis (default: 5s).
- `--layout [layout1, layout2]`  
  Test based on layouts.
- `--layout-id [layout id1, layout id2]`  
  Test based on layouts IDs.
- `--site [site1, site2]`  
  Test based on sites.
- `--site-id [site id1, site id2]`  
  Test based on site IDs.
- `-t, --table`  
  Display result in table format.
- `--tag [tag1, tag2]`  
  Test based on tags.
- `--time`  
  Display the execution time of the command.

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

### live-video-latency

Get test results live video latency

#### Options

- `-a, --all-log`
  Display execution logs.
- `-b, --bridge [bridge1, bridge2]`
  Test based on bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`
  Test based on bridge ESNs.
- `-c, --count [count]`
  Number of videos frames to be tested (default: 3).
- `-C, --camera [camera1, camera2]`
  Test based on cameras.
- `--call-time`
  Get api response time.
- `--csv`
  List details in csv format.
- `-d, --debug`
  Enable detailed debug output for troubleshooting.
- `--esn [esn1, esn2]`
  Test based on camera ESNs.
- `-f, --file-name [file name]`
  Specify the file name to save the test results.
- `-g, --google-sheet`
  List details in csv format in google sheet.
- `--header`
  Display column headers in the result.
- `--layout [layout1, layout2]`
  Test based on layouts.
- `--layout-id [layout id1, layout id2]`
  Test based on layouts IDs.
- `--prompt`
  Show user confirmation prompts (default: false).
- `--site [site1, site2]`
  Test based on sites.
- `--site-id [site id1, site id2]`
  Test based on site IDs.
- `--tag [tag1, tag2]`
  Test based on tags.
- `--time`
  Display the execution time of the command.

## EXAMPLES

- To test live video latency of all the cameras in an account:

```bash
een perftest live-video-latency
```

- To test live video latency of all the cameras in a specific bridge:

```bash
een perftest live-video-latency --bridge-esn "<bridge_id>"
```

### historic

Get performance test results for history video.

#### Options

- `-a, --all-log`  
  Display execution logs.
- `--bridge [bridge1, bridge2]`  
  Test based on bridges.
- `--bridge-esn [bridge esn1, bridge esn2]`  
  Test based on bridge ESNs.
- `-c, --count [count]`  
  Number of previews to be tested (default: 5).
- `-C, --camera [camera1, camera2]`  
  Test based on cameras.
- `--call-time`  
  Get api response time.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Specify the end timestamp for analysis, this option requires --start-time to be specified.
- `--esn [esn1, esn2]`  
  Test based on camera ESNs.
- `-f, --file-name [file name]`  
  Specify the file name to save the test results.
- `--header`  
  Display column headers in the result.
- `-l, --length`  
  Specify the video duration for analysis (default: 10s).
- `--layout [layout1, layout2]`  
  Test based on layouts.
- `--layout-id [layout id1, layout id2]`  
  Test based on layouts IDs.
- `-s, --start-time [start time]`  
  Specify the start timestamp for analysis.
- `--site [site1, site2]`  
  Test based on sites.
- `--site-id [site id1, site id2]`  
  Test based on site IDs.
- `-t, --table`  
  Display result in table format.
- `--tag [tag1, tag2]`  
  Test based on tags.
- `--time`  
  Display the execution time of the command.

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

## COMMANDS

### update

Update Google config option values.

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

### Camera settings that can be edited:

1. cloud-retention-days - [Cloud retention]
2. video-resolution - [Video resolution]
3. bridge-target-days - [Local retention - Min]
4. local-retention-days - [Local retention - Max]
5. preview-resolution - [Preview resolution]
6. preview-transmit-mode - [Preview transmit mode]
7. video-transmit-mode - [Video transmit mode]
8. video-quality - [Full Video quality]
9. tags - [Tags]
10. username - [Camera username]
11. password - [Camera password]
12. aspect-ratio- [Preview aspect ratio]
13. video-capture-mode - [Preview Record when]
14. preview-interval-ms - [Preview update rate]
15. preview-quality - [Preview quality]
16. preview-only-cloud-retention - [Cloud Preview Only (PR1)]
17. audio-enable - [Enable audio if available]
18. audio-disable - [Disable audio if available]

Note:

- Except for `cameraID` and `cameraName` all other fields in the camera settings file are editable.

### Bridge settings that can be edited:

1. local-rtsp-metrics - [Bridge rtsp metrics]

### Available camera status

- "Camera online"
- "Stream attached"
- "Camera on"
- "Camera recording"
- "Camera sending previews"
- "Camera located"
- "Camera not supported"
- "Camera configuration in process"
- "Camera needs ONVIF password"
- "Camera available but not yet attached"
- "Internal status"
- "Camera error"
- "Reserved"
- "Invalid state"
- "Camera streaming"
- "Camera registered"

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
