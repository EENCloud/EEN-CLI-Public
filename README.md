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

- For all commands with `--no-prompt` option it will skip all user confirmation prompts. This means it will also overwrite any existing files without any confirmation.
- Open all the CSV file outputs in Google Sheets or Libre Office as Excel has formatting issues.
- `verbose mode` : Use `--verbose` along with the commands to access the verbose mode.
- Supported `EEN TIME FORMATS` :

  - 20230125062511.000
  - 2023-01-31
  - 2023-01-31T08:24:32
  - 2023-10-02T23:50:06.337+00:00

- Execute this extracted file by mapping up the directory path of the een
  on the terminal
- Each command should start `./`.

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

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.

#### Notes:

- If the shell misinterprets special characters, ensure the password is wrapped in quotes.

---

### logout

Log out from EEN.

#### Options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.

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
- `--html`  
  Generate an HTML report for user permissions.
- `-l, --long`  
  Display user details, including name, email, last login, status, and permissions.
- `-L, --last-name`  
  Display user last names.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-p, --permission`  
  Display user permissions.
- `-s, --status`  
  Display user statuses.
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

List all accounts of the reseller account.

#### Options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-l, --long`  
  Display account details, including account ID, account name, and account type.
- `--account-id [account ID]`  
  Specify an account ID to list its details.
- `-s, --sub-account-id`  
  List sub-accounts (only applicable for reseller accounts).

---

### switch

Switch to an account.

#### Options:

- `-a, --account-id [account ID]`  
  Specify the Account ID to switch between logged-in accounts.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-s, --sub-account-id [sub-account ID]`  
  Specify the Sub Account ID to switch to from the reseller account.

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

- `--csv`  
  Export the archive list in CSV format.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-D, --detailed`  
  Retrieve a detailed list of archives with additional metadata.
- `-l, --long`  
  Display archive details, including filename, size, creation date, shared status, and shared path.
- `-t, --target-directory [target directory]`  
  Specify the directory from which the archive will be retrieved.

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

- `-d, --debug`  
  Enable debug output for troubleshooting.
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

- `-a, --all`  
  List all cameras without filtering.
- `-A, --available`  
  List available cameras that are currently operational.
- `-b, --bridge-esn`  
  List cameras by their bridge ESNs.
- `-c, --cloud-retention-days`  
  List cameras filtered by their cloud retention days.
- `--csv`  
  List cameras in CSV format.
- `-d, --debug`  
  Enable debug output for troubleshooting and detailed logs.
- `-e, --end-time [end time]`  
  Filter cameras based on video end time. Format: `YYYYMMDDHHMMSS.sss` (Compact ISO 8601 date-time with milliseconds).
- `--esn`  
  List cameras by their ESNs.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved. This can be used with `--csv` or `--google-sheet`.
- `-g, --google-sheet`  
  List cameras in CSV format in a Google Sheet.
- `--html`  
  Generate a chart of the camera list in an HTML file format.
- `-l, --long`  
  List camera details, including camera ESN, bridge ESN, status, resolution, cloud retention days, and local retention days.
- `-L, --local-retention-days`  
  List cameras filtered by their local retention days.
- `-n, --no-prompt`  
  Skip all user confirmation prompts during the command execution.
- `-p, --purge`  
  The `--purge` option only works with `--csv` or `--google-sheet` options. It removes expired data from the output.
- `--v1`  
  Use version 1 APIs for backward compatibility.
- `-r, --resolution`  
  List cameras filtered by resolution.
- `-s, --sites [site1, site2...]`  
  List cameras located in the specified sites. Provide a comma-separated list of site names.
- `-S, --start-time [start time]`  
  Filter cameras based on video start time. Format: `YYYYMMDDHHMMSS.sss` (Compact ISO 8601 date-time with milliseconds).
- `--shared`  
  List cameras that are shared with other users.
- `--short`  
  List only the camera names and ESNs in CSV format to the specified file.
- `--status [status]`  
  List cameras with a specific status. Accepts values like 'online', 'offline', or 'inactive'.
- `-t, --tags [tag1, tag2...]`  
  List cameras based on the given tag. Specify the tag as a comma-separated list of tag names.
- `-T, --tree`  
  List cameras and associated bridges in a tree format.

#### Notes:

- Start-time and end-time must follow the format: `YYYYMMDDHHMMSS.sss` (Compact ISO 8601 date-time with milliseconds).

---

### status

List status of all cameras.

#### Options:

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
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `--v1`  
  Use v1 APIs.

---

### settings

Get all camera settings.

#### Required options:

- `--csv`  
  List camera settings in CSV format.

#### Optional options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.

---

### set

Edit camera's settings.

#### Arguments:

- `-b, --bridge-esns [bridge-esns]`  
  Edit camera settings by bridge ESNs.
- `--esns [esn1, esn2...]`  
  Edit camera settings by camera ESNs.
- `-f, --file-name [file name]`  
  Edit camera settings by reading the CSV file.
- `-T, --tags [tags]`  
  Edit camera settings by tag.
- `-s, --site-id [site-id]`  
  Edit camera settings by site id.
- `-S, --site-name [site-name]`  
  Edit camera settings by site name.
- `--layout-name [layout-name]`  
  Edit camera settings by layout name.
- `--layout-id [layout-id]`  
  Edit camera settings by layout id.

#### Options:

- `-a, --aspect-ratio [aspect ratio]`  
  Preview aspect ratio.
- `--audio-enable`  
  Enable audio.
- `--audio-disable`  
  Disable audio.
- `-B, --bridge-target-days [bridge target days]`  
  Bridge target days.
- `-c, --cloud-retention-days [cloud retention days]`  
  Cloud retention days.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-l, --local-retention-days [local retention days]`  
  Local retention days.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-p, --password [password]`  
  Password.
- `--preview-resolution [preview resolution]`  
  Preview resolution.
- `--preview-transmit-mode [preview transmit mode]`  
  Preview transmit mode.
- `--preview-interval-ms [preview interval ms]`  
  Preview interval rate in milliseconds.
- `--preview-quality [preview quality]`  
  Preview quality.
- `--preview-only-cloud-retention [preview only cloud retention]`  
  Preview only cloud retention.
- `-t, --add-tag [add tag]`  
  Tags.
- `-u, --username [username]`  
  Username.
- `--video-capture-mode [video capture mode]`  
  When to record video.
- `--video-transmit-mode [video transmit mode]`  
  Video transmit mode.
- `--video-quality [video quality]`  
  Video quality.
- `--video-resolution [video resolution]`  
  Video resolution.

---

#### Notes:

- For `--esns "*"`, it changes settings for all cameras.

### delete

Delete a camera from the bridge.

#### Argument:

- `<esn>`  
  ESN of the camera (required)

#### Options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.

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
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-p, --password [password]`  
  Camera password.
- `-s, --site [site]`  
  Site ID.
- `-S, --scene [scene]`  
  Scene.
- `-t, --tags [tags]`  
  Tags.
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

- `--esns [esn1, esn2...]`  
  ESNs of the cameras.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-S, --stream-type [stream type]`  
  Stream type of the camera.

#### Notes:

- `stream-type` can be **"fullvideo"** or **"preview"**.
- `start-time` can be **"-1h"** (one hour before current time).
- `end-time` can be **"now"** (current time).
- `start-time` and `end-time` time format should be `YYYYMMDDHHMMSS.sss` (Compact ISO 8601 date time with millisecond precision).

---

### purgelist

Get camera purging and duty cycle.

#### Options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Purge end time.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-s, --start-time [start time]`  
  Purge start time.

#### Notes:

- If you haven't specified any start-time and end-time, it will take the last 24 hours as default timestamps.
- `start-time` and `end-time` time format should be `YYYYMMDDHHMMSS.sss` (Compact ISO 8601 date time with millisecond precision).

---

### availability

Get camera availability.

#### Required options:

- `--esns [esn1, esn2...]`  
  ESNs of the camera.
- `--start-time [start time]`  
  Video start time.

#### Optional options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Video end time.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List camera availability in CSV format in Google Sheets.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-N, --no-check`  
  Show all available data, including unchecked items.
- `-p, --preview-availability`  
  Get preview recording status along with camera availability.
- `-s, --start-time [start time]`  
  Video start time.

#### Notes:

- This command only supports a maximum of 200 devices and a seven-day time range.
- `start-time` and `end-time` time format should be `YYYY-MM-DDTHH:MM:SS.sss±HH:MM` (ISO 8601 extended date-time).

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
- `--html`  
  Generate a chart in HTML file.
- `-l, --long`  
  Display bridge details, including bridge ID, name, and location. For v3, also includes cameras in the account and online cameras; for v1, includes GUID.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-s, --site`  
  List the site of the bridge.
- `--sites [site1, site2...]`  
  List bridges in a specific site.
- `-S, --status [status]`  
  List bridges with a specific status.
- `-t, --tags [tag1, tag2...]`  
  Filter bridges by tags.
- `-T, --tree`  
  View bridges and associated cameras in tree format.
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

- `-d, --debug`  
  Enable detailed debug output for troubleshooting
- `-g, --google-sheet`  
  List bridges in csv format in a Google Sheet
- `--html`  
  Generate a chart in an HTML file

---

### availability

Get bridge availability.

#### Required options:

- `-e, --end-time [end time]`  
  Specify video end time
- `--esns [esn1, esn2...]`  
  ESNs of the bridge

#### Optional options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting
- `-f, --file-name [file name]`  
  Specify the file name to save the output
- `-g, --google-sheet`  
  List bridge availability in csv format in a Google Sheet
- `-n, --no-prompt`  
  Skip all user confirmation prompts
- `-N,. --no-check`  
  Show all available data
- `-s, --start-time [start time]`  
  Specify video start time

---

### qlstreammetrics

Pull logs from the archiver/bridge.

#### Required options:

- `--esns [esn1, esn2...]`  
  Esns of the bridge (required).

#### Optional options:

- `-c, --count [count]`  
  Specify the number of annotations to return
- `-d, --debug`  
  Enable detailed debug output for troubleshooting
- `-e, --end-time [end time]`  
  Specify the end time
- `-E, --events`  
  View events of the bridge
- `-l, --local-rtsp-metrics [enable/disable]`  
  Enable or disable the RTSP metrics set
- `-n, --no-prompt`  
  Skip all user confirmation prompts
- `-p, --performance`  
  View performance metrics of the bridge
- `-s, --start-time [start time]`  
  Specify the start time
- `-S, --summary`  
  Get summarized data

#### Notes:

- start-time and end-time time format should be YYYYMMDDHHMMSS.sss (Compact ISO 8601 date time with millisecond precision)

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
een bridge availability --esns [esns] --start-time [start time] --end-time [end time]
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
  List the bridge ESNs associated with the switches
- `-d, --debug`  
  Enable detailed debug output for troubleshooting
- `--id`  
  List the IDs of the switches
- `-l, --long`  
  List switch details, including switch ID, bridge ESN, and status
- `-s, --status`  
  List the status of the switches

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

- `-a, --address`  
  List the site addresses.
- `--csv`  
  List all sites in CSV format.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-l, --long`  
  List site details, including site name and site ID.
- `-s, --site-id`  
  List the IDs of the sites.
- `-S, --site-name`  
  List the site names.

#### Actions:

- List sites with options for CSV format, file output, skipping prompts, and debug output as specified.

## EXAMPLES

- To list all sites in CSV format:

```bash
een site list --csv --file-name sites.csv
```

- To list sites without prompting for confirmation:

```bash
een site list --no-prompt --debug
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

- `--esn [esn]`  
  ESN of the camera.
- `-e, --end-time [end time]`  
  Video end time.
- `-f, --format [format]`  
  Video format.
- `-s, --start-time [start time]`  
  Video start time.
- `-t, --target-directory [target-directory]`  
  Specify the directory where the video will be saved.

#### Optional options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-o, --overwrite`  
  Overwrite the existing video file.
- `-T, --timezone [timezone]`  
  Timezone to use for the video download.

#### Notes:

- Video downloads support both mp4 and FLV formats.
- The timezone option is only supported for mp4 format.
- Video downloading is done in batches of 5 videos at a time.
- start-time and end-time time format should be YYYYMMDDHHMMSS.sss (Compact ISO 8601 date time with millisecond precision)

#### Actions:

- Downloads the video from the specified camera if all required options are provided.

---

### list

Get a list of videos from the selected camera.

#### Required options:

- `--esn [esn]`  
  ESN of the camera.
- `-s, --start-time [start time]`  
  Video start time.
- `-e, --end-time [end time]`  
  Video end time.

#### Optional options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.

#### Notes:

- start-time and end-time time format should be YYYYMMDDHHMMSS.sss (Compact ISO 8601 date time with millisecond precision)

#### Actions:

- Lists videos available from the specified camera within the given time frame.

---

### previewrecordingstatus

Get the status of preview recording.

#### Required options:

- `--esns [esns]`  
  ESNs of the camera.
- `-s, --start-time [start time]`  
  Video start time.

#### Optional options:

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-e, --end-time [end time]`  
  Video end time.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-g, --google-sheet`  
  List camera recording status in CSV format in Google Sheets.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.

#### Notes:

- start-time and end-time time format should be YYYY-MM-DDTHH:MM:SS.sss±HH:MM (ISO 8601 extended date-time)

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
een video previewrecordingstatus --esns 1005f355 --start-time  2024-11-17T09:20:54.619+00:00 --end-time  2024-11-18T09:20:54.619+00:00 --debug
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

- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--esns [esn1, esn2...]`  
  The ESN for camera of interest.
- `--lp [license plate]`  
  License plate number.
- `--v1`  
  Use v1 APIs.

#### Notes:

- start-time and end-time time format should be YYYYMMDDHHMMSS.sss (Compact ISO 8601 date time with millisecond precision)

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
- `-b, --body-types [types]`  
  Vehicle body types.
- `-c, --colors [colors]`  
  Vehicle colors.
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-D, --directions [directions]`  
  Direction of the vehicle.
- `-e, --end-time [end time]`  
  LPR end time.
- `--esns [esns]`  
  Camera ESNs.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--html`  
  Generate chart in HTML file.
- `--lp [lp]`  
  License plate number.
- `-m, --makes [makes]`  
  Vehicle makes.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-s, --sites [sites]`  
  Site names.
- `-S, --start-time [start time]`  
  LPR start time.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.
- start-time and end-time time format should be YYYYMMDDHHMMSS.sss (Compact ISO 8601 date time with millisecond precision).

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
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `-D, --denied-vehicle`  
  Alert type - denied vehicle.
- `-e, --end-time [end time]`  
  LPR end time.
- `--esns [esns]`  
  Camera ESN.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--html`  
  Generate chart in HTML file.
- `-H, --hotlist`  
  Alert type - hotlist.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `-s, --sites [sites]`  
  Name of the site.
- `-S, --start-time [start time]`  
  LPR start time.
- `-u, --unregistered-vehicle`  
  Alert type - unregistered vehicle.
- `-w, --watch-vehicle`  
  Alert type - watch vehicle.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.
- start-time and end-time time format should be YYYY-MM-DDTHH:MM:SS.sss±HH:MM (ISO 8601 extended date-time).

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
- `-d, --debug`  
  Enable detailed debug output for troubleshooting.
- `--discount-min [discount min]`  
  Specify the minimum discount in percentage.
- `--discount-max [discount max]`  
  Specify the maximum discount in percentage.
- `-e, --end-time [end time]`  
  Defines the end point for retrieving events. The timestamp must be in ISO 8601 format with millisecond precision (e.g., YYYY-MM-DDTHH:MM:SS.sss±HH:MM).
- `-E, --employee-id [employee ID]`  
  Specify the ID of the employee.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `-F, --flagged`  
  Retrieve flagged transactions.
- `--html`  
  Generate chart in HTML file.
- `-n, --no-prompt`  
  Skip all user confirmation prompts.
- `--net-amount-min [net amount min]`  
  Specify the minimum net amount.
- `--net-amount-max [net amount max]`  
  Specify the maximum net amount.
- `-s, --sites [sites]`  
  Specify the name of the site.
- `-S, --start-time [start time]`  
  Defines the starting point for retrieving events. The timestamp must be in ISO 8601 format with millisecond precision (e.g., YYYY-MM-DDTHH:MM:SS.sss±HH:MM).
- `-t, --transaction-type [transaction type]`  
  Specify the type of the transaction.

#### Notes:

- If no start time or end time is specified, the retrieval period defaults to the last 24 hours.
- Start-time and end-time time format should be YYYY-MM-DDTHH:MM:SS.sss±HH:MM (ISO 8601 extended date-time).

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
