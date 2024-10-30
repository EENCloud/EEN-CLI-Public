# Introduction

## Latest CLI Version

The latest CLI release version: ![Latest Release](https://img.shields.io/github/v/release/EENCloud/EEN-CLI-Public)

## Environment variables

<a name="environment-variables"></a>

1. `API_KEY`

   - Creation: To get an `API_KEY` you will need an account. You can either use your existing account or create a Developer Account.

     - Existing account: You can create the key under your Account Settings.
     - Developer account: You will have to verify your email address first to create your Developer Account. Expect to get an email with a shortcut to create the `API_KEY`. Click on the shortcut link to create your `API_KEY` and get started writing some code.

## Using the CLI

## Setting-up of Executable File

- Extraction of file from a compressed file format

  #### **In Linux:**

  - There are multiple ways to extract file from a compressed file here are the step by step instruction:

  - First way:

    1. Point the cursor on the compressed file.
    2. Right-click on it in-order to trigger context-menu(right-click menu).
    3. On context menu select `Extract Here` option to extract the file in same directory or
       Select `Extract to` option in-order to extract the file in the current directory or directory of your choice.

  - Second way:

    1. Point the cursor on the compressed file.
    2. Left-Double-click on it in-order to trigger a window that shows extraction option.
    3. Select the `Extract` button in-order to extract the file in desired directory.

  - Third way:
    1. Open the terminal in the directory where compressed file is stored.
    2. Type-in terminal command `unzip een.zip` in-order to extract the file in the current directory.
    ```
    unzip een.zip
    ```

  #### **In Windows:**

  - Here are the step by step instruction:
    1. Point the cursor on the compressed file.
    2. Right-click on it in-order to trigger context-menu(right-click menu).
    3. On context menu select `Extract All`.
    4. A window is triggered that shows a input-box which is used to inserts the directory path to a choosen directory.
    5. After choosing a directory click on `Extract` button, in-order to extract the file to the choosen directory.

<br/>

#### Notes:

- For all commands with `--no-prompt` option it will skip all user confirmation prompts. This means it will also overwrite any existing files without any confirmation.
- Open all the CSV file outputs in google sheet or libre office as excel has formatting issues.
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
    'een <command> help' lists the usage with opitions and descriptions
  ```

# EEN Command Line Interface Manual

## NAME

`een` - A command-line tool for managing and retrieving information related to cameras, bridges, users, and more in a cloud-based environment.

## SYNOPSIS

```
een [OPTIONS] <object> <command> [ARGS]
```

## DESCRIPTION

The **een** CLI provides various commands to interact with cameras, bridges, users, locations, and other resources. It offers multiple options for fetching information in different formats (CSV, tree structure, etc.) and supports both standard and v3 APIs.

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

The **een auth** command provides utilities for logging in and logging out of the EEN (Eagle Eye Networks).

## COMMANDS

### login

Log in to EEN using the provided credentials.

#### Required options:

- `--user-name [user name]`  
  The username used for login.
- `--password [password]`  
  The password used for login.

#### Optional options:

- `--api-key [api key]`  
  API key used for login.
- `--verbose`  
  Enable verbose output.

#### Notes:

- Password should be given in quotes, as the shell might have converting issues.

---

### logout

Log out from EEN.

#### Options:

- `--verbose`  
  Enable verbose output.

## EXAMPLES

- To login

```bash
een auth login --user-name johndoe --password secret --verbose
```

- To logout

```bash
een auth logout --verbose
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
  List all users in CSV format.
- `--google-sheet`  
  List users in CSV format in Google Sheets.
- `--v3`  
  Use v3 APIs.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--html`  
  Generate chart in HTML file.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.

#### Actions:

- If `--html` is specified, generate user permission report.
- If `--csv` and `--v3` are specified, list users in CSV format using v3.
- If `--csv` is specified, list users in CSV format.
- If `--google-sheet` is specified, list user permissions in Google Sheets.
- If `--v3` is specified, list users using v3 APIs.

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

The `account` command allows you to manage reseller accounts, including listing all accounts and switching between sub-accounts.

## COMMANDS

### list

List all accounts of the reseller account.

#### Options:

- `--verbose`  
  Enable verbose output.

---

### switch

Switch to a sub-account.

#### Options:

- `--sub-account-id [sub-account id]`  
  Account ID to which we need to switch (required).
- `--verbose`  
  Enable verbose output.

## EXAMPLES

- To list all accounts of the reseller:

```bash
een account list --verbose
```

- To switch to a specific sub-account:

```bash
een account switch --sub-account-id <sub-account id> --verbose
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

- `--detailed`  
  Get a detailed archive list.
- `--csv`  
  List all archives in CSV format.
- `--target-directory [target directory]`  
  Specify the name of the directory where the output will be saved.

- `--verbose`  
  Enable verbose output.

---

### download

Download a specific archive.

#### Arguments:

- `<archive>`  
  The name of the archive to download (required).

#### Required options:

- `--target-directory [target-directory]`  
  Specify the name of the directory where the output will be saved.

#### Optional options:

- `--overwrite`  
  Overwrite already downloaded archive.
- `--verbose`  
  Enable verbose output.

## EXAMPLES

- To list available archives:

```bash
een archive list --detailed --csv --target-directory /path/to/output
```

- To download a specific archive:

```bash
een archive download <archive> --target-directory /path/to/save --overwrite --verbose
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

- `--csv`  
  List cameras in CSV format.
- `--tree`  
  List cameras and associated bridges in tree format.
- `--tags [tags]`  
  List cameras based on the given tag.
- `--available`  
  List available cameras.
- `--locations [locations]`  
  List cameras in a given location.
- `--status [status]`  
  List cameras with a specific status.
- `--short`  
  List camera name and ESN in CSV format to the given file.
- `--html`  
  Generate chart in HTML file.
- `--google-sheet`  
  List bridges in CSV format in Google Sheet.
- `--purge`  
  The `--purge` option only exists with either `--csv` or `--google-sheet`.
- `--start-time [start time]`  
  Video start time.
- `--end-time [end time]`  
  Video end time.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.
- `--v3`  
  Use v3 APIs.

---

### status

List status of all cameras.

#### Options:

- `--csv`  
  List camera status in CSV format.
- `--html`  
  Generate chart in HTML file.
- `--google-sheet`  
  List camera status in CSV format in Google Sheet.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.

---

### settings

Get all the camera settings.

#### Required options:

- `--csv`  
  List camera settings in CSV format.

#### Optional options:

- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.

---

### set

Edit a single camera's settings.

#### Arguments:

- `<esn>`  
  Camera ESN.

#### Options:

- `--cloud-retention-days [cloud retention days]`  
  Cloud retention days.
- `--video-resolution [video resolution]`  
  Video resolution.
- `--bridge-target-days [bridge target days]`  
  Bridge target days.
- `--local-retention-days [local retention days]`  
  Local retention days.
- `--preview-resolution [preview resolution]`  
  Preview resolution.
- `--preview-transmit-mode [preview transmit mode]`  
  Preview transmit mode.
- `--video-transmit-mode [video transmit mode]`  
  Video transmit mode.
- `--video-quality [video quality]`  
  Video quality.
- `--tags [tags]`  
  Tags.
- `--user-name [user name]`  
  Username.
- `--password [password]`  
  Password.
- `--aspect-ratio [aspect ratio]`  
  Preview aspect ratio.
- `--video-capture-mode [video capture mode]`  
  When to record video.
- `--preview-interval-ms [preview interval ms]`  
  Preview interval rate in milliseconds.
- `--preview-quality [preview quality]`  
  Preview quality.
- `--preview-only-cloud-retention [preview only cloud retention]`  
  Preview only cloud retention.
- `--audio-enable`  
  Enable audio.
- `--audio-disable`  
  Disable audio.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.

---

### bulkset

Edit multiple camera settings.

#### Required options:

- `--esns [esns]`  
  camera esns which is camera ID

#### Optional options:

- `--cloud-retention-days [cloud retention days]`  
  cloud retention days
- `--video-resolution [video resolution]`  
  video resolution
- `--bridge-target-days [bridge target days]`  
  bridge target days
- `--local-retention-days [local retention days]`  
  local retention days
- `--preview-resolution [preview resolution]`  
  preview resolution
- `--preview-transmit-mode [preview transmit mode]`  
  preview transmit mode
- `--video-transmit-mode [video transmit mode]`  
  video transmit mode
- `--video-quality [video quality]`  
  video quality
- `--tags [tags]`  
  tags
- `--user-name [user name]`  
  username
- `--password [password]`  
  password
- `--aspect-ratio [aspect ratio]`  
  preview aspect ratio
- `--video-capture-mode [video capture mode]`  
  when to record video
- `--preview-interval-ms [preview interval ms]`  
  preview interval rate in milliseconds
- `--preview-quality [preview quality]`  
  preview quality
- `--preview-only-cloud-retention [preview only cloud retention]`  
  preview only cloud retention
- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output
- `--audio-enable`  
  audio enable
- `--audio-disable`  
  audio disable

---

### tagset

Edit camera settings based on a specific tag.

#### Required options:

- `--tag [tag]`  
  camera tag

#### Optional options:

- `--cloud-retention-days [cloud retention days]`  
  cloud retention days
- `--video-resolution [video resolution]`  
  video resolution
- `--bridge-target-days [bridge target days]`  
  bridge target days
- `--local-retention-days [local retention days]`  
  local retention days
- `--preview-resolution [preview resolution]`  
  preview resolution
- `--preview-transmit-mode [preview transmit mode]`  
  preview transmit mode
- `--video-transmit-mode [video transmit mode]`  
  video transmit mode
- `--video-quality [video quality]`  
  video quality
- `--tags [tags]`  
  tags
- `--user-name [user name]`  
  username
- `--password [password]`  
  password
- `--aspect-ratio [aspect ratio]`  
  preview aspect ratio
- `--video-capture-mode [video capture mode]`  
  when to record video
- `--preview-interval-ms [preview interval ms]`  
  preview interval rate in milliseconds
- `--preview-quality [preview quality]`  
  preview quality
- `--preview-only-cloud-retention [preview only cloud retention]`  
  preview only cloud retention
- `--audio-enable`  
  audio enable
- `--audio-disable`  
  audio disable
- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output

---

### multiset

Edit all camera settings.

#### Options:

- `--cloud-retention-days [cloud retention days]`  
  cloud retention days
- `--video-resolution [video resolution]`  
  video resolution
- `--bridge-target-days [bridge target days]`  
  bridge target days
- `--local-retention-days [local retention days]`  
  local retention days
- `--preview-resolution [preview resolution]`  
  preview resolution
- `--preview-transmit-mode [preview transmit mode]`  
  preview transmit mode
- `--video-transmit-mode [video transmit mode]`  
  video transmit mode
- `--video-quality [video quality]`  
  video quality
- `--tags [tags]`  
  tags
- `--user-name [user name]`  
  username
- `--password [password]`  
  password
- `--aspect-ratio [aspect ratio]`  
  preview aspect ratio
- `--video-capture-mode [video capture mode]`  
  when to record video
- `--preview-interval-ms [preview interval ms]`  
  preview interval rate in milliseconds
- `--preview-quality [preview quality]`  
  preview quality
- `--preview-only-cloud-retention [preview only cloud retention]`  
  preview only cloud retention
- `--audio-enable`  
  audio enable
- `--audio-disable`  
  audio disable
- `-f, --file-name [file name]`  
  specify the name of the file where the output will be saved (required)
- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output

---

### detailedset

Edit camera settings taking values from a CSV file.

#### Required options:

- `-f, --file-name [file name]`  
  specify the name of the CSV file

#### Optional options:

- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output

---

### delete

Delete a camera from the bridge.

#### Argument:

- `<esn>`  
  esn of the camera (required)

#### Options:

- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output

---

### add

Add camera to bridge.

#### Argument:

- `<esn>`  
  esn of the bridge to which the camera is added

#### Required options:

- `--camera-name [camera name]`  
  name of the camera
- `--guid [guid]`  
  guid of the camera

#### Optional options:

- `--cloud-retention-days [cloud retention days]`  
  cloud retention days
- `--scene [scene]`  
  scene
- `--tags [tags]`  
  tags
- `--user-name [user name]`  
  username
- `--password [password]`  
  password
- `--location [location]`  
  location id
- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output

---

### streamstatus

Get camera stream status.

#### Arguments:

- `<esns>`  
  esns of the camera

#### Required options:

- `--start-time [start time]`  
  camera stream start time
- `--end-time [end time]`  
  camera stream end time

#### Optional options:

- `--stream-type [stream type]`  
  stream type of the camera
- `-f, --file-name [file name]`  
  specify the name of the file where the output will be saved
- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output

#### Notes:

- stream-type can be **"fullvideo"** or **"preview"**
- start-time can be **"-1h"** i.e., one hour before current time
- end-time can be **"now"** i.e., current time

---

### purgelist

Get camera purging and duty cycle.

#### Options:

- `--start-time [start time]`  
  purge start time
- `--end-time [end time]`  
  purge end time
- `-f, --file-name [file name]`  
  specify the name of the file where the output will be saved
- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output

#### Notes:

- If you haven't specified any start-time and end-time it will take the last 24 hours as default timestamps.

---

### availability

Get camera availability.

#### Required options:

- `--esns [esns]`  
  esns of the camera

#### Optional options:

- `--start-time [start time]`  
  video start time
- `--end-time [end time]`  
  video end time
- `-f, --file-name [file name]`  
  specify the name of the file where the output will be saved
- `--google-sheet`  
  list camera availability in CSV format in Google Sheets
- `--preview-availability`  
  get preview recording status along with camera availability
- `--no-prompt`  
  skip all user confirmation prompts
- `--verbose`  
  enable verbose output

#### Notes:

- This command only supports a maximum of 200 devices and seven days of time range.

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

- `--csv`  
  List all bridges in CSV format.
- `--tree`  
  List bridges and associated cameras in tree format.
- `--available`  
  List discovered cameras that are not yet attached.
- `--locations [locations]`  
  List bridges in a given location.
- `--tags [tags]`  
  List bridges based on the given tag.
- `--status [status]`  
  List bridges with a specific status.
- `--html`  
  Generate chart in HTML file.
- `--google-sheet`  
  List bridges in CSV format in Google Sheet.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.
- `--v3`  
  Use v3 APIs.

#### Actions:

- If `--html` is specified and `--v3`, generate bridge list report using v3.
- If `--csv` is specified and `--v3`, list bridges in CSV format using v3.
- Handle other combinations of options to perform various listing and reporting tasks.

---

### status

List bridge status.

#### Options:

- `--html`  
  Generate chart in HTML file.
- `--google-sheet`  
  List bridges in CSV format in Google Sheet.
- `--verbose`  
  Enable verbose output.

---

### availability

Get bridge availability.

#### Required options:

- `--esns [esns]`  
  ESN of the bridge.

#### Options:

- `--start-time [start time]`  
  Video start time.
- `--end-time [end time]`  
  Video end time.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--google-sheet`  
  List bridge availability in CSV format in Google Sheet.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.

---

### qlstreammetrics

Pull logs from the archiver/bridge.

#### Required options:

- `--esns [esns]`  
  ESNs of the bridge (required).

#### Optional options:

- `--performance`  
  Performance of the bridge.
- `--events`  
  Events of the bridge.
- `--count [count]`  
  Number of annotations to return.
- `--start-time [start time]`  
  Start time.
- `--end-time [end time]`  
  End time.
- `--summary`  
  Get summarized data.
- `--local-rtsp-metrics [enable/disable]`  
  Enable or disable metric set.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.

---

### updatecameras

Update all cameras under the bridge(s).

#### Required options:

- `--esns [esns]`  
  ESN of the bridge (required).

#### Optional options:

- `--cloud-retention-days [cloud retention days]`  
  Cloud retention days.
- `--video-resolution [video resolution]`  
  Video resolution.
- `--bridge-target-days [bridge target days]`  
  Bridge target days.
- `--local-retention-days [local retention days]`  
  Local retention days.
- `--preview-resolution [preview resolution]`  
  Preview resolution.
- `--preview-transmit-mode [preview transmit mode]`  
  Preview transmit mode.
- `--video-transmit-mode [video transmit mode]`  
  Video transmit mode.
- `--video-quality [video quality]`  
  Video quality.
- `--tags [tags]`  
  Tags.
- `--user-name [user name]`  
  Username.
- `--password [password]`  
  Password.
- `--aspect-ratio [aspect ratio]`  
  Preview aspect ratio.
- `--video-capture-mode [video capture mode]`  
  When to record video.
- `--preview-interval-ms [preview interval ms]`  
  Preview interval rate in milliseconds.
- `--preview-quality [preview quality]`  
  Preview quality.
- `--preview-only-cloud-retention [preview only cloud retention]`  
  Preview only cloud retention.
- `--audio-enable`  
  Audio enable.
- `--audio-disable`  
  Audio disable.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.

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

# location - Manage Locations

## NAME

`location` - manage and interact with locations.

## SYNOPSIS

```
een location [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `location` command allows you to manage locations, including listing all available locations.

## COMMANDS

### list

List all locations.

#### Options:

- `--csv`  
  List all locations in CSV format.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--verbose`  
  Enable verbose output.

#### Actions:

- List locations with options for CSV format, file output, skipping prompts, and verbose output as specified.

## EXAMPLES

- To list all locations in CSV format:

```bash
een location list --csv --file-name locations.csv
```

- To list locations without prompting for confirmation:

```bash
een location list --no-prompt --verbose
```

# video - Manage Camera Videos

## NAME

`video` - manage and interact with videos from cameras.

## SYNOPSIS

```
een video [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `video` command allows you to download videos from cameras, list available videos, and check the status of preview recordings.

## COMMANDS

### download

Download video from the camera.

#### Required options:

- `--esn [esn]`  
  ESN of the camera.
- `--start-time [start time]`  
  Video start time.
- `--end-time [end time]`  
  Video end time.
- `--format [format]`  
  Video format.
- `--target-directory [target-directory]`  
  Specify the name of the directory where the output will be saved.

#### Optional options:

- `--timezone [timezone]`  
  Timezone.
- `--overwrite`  
  Overwrite already downloaded video.
- `--verbose`  
  Enable verbose output.

#### Notes:

- For video download, support both mp4 and FLV format.
- The timezone option is only supported for mp4 format.
- Video download is done by batches of 5 videos at a time.

#### Actions:

- Downloads the video from the specified camera if all required options are provided.

---

### list

Get camera video list.

#### Required options:

- `--esn [esn]`  
  ESN of the camera.
- `--start-time [start time]`  
  Video start time.
- `--end-time [end time]`  
  Video end time.

#### Optional options:

- `--verbose`  
  Enable verbose output.

#### Actions:

- Lists videos available from the specified camera within the given time frame.

---

### previewrecordingstatus

Get the status of preview recording.

#### Required options:

- `--esns [esns]`  
  ESNs of the camera.
- `--start-time [start time]`  
  Video start time.

#### Optional options:

- `--end-time [end time]`  
  Video end time.
- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.
- `--no-prompt`  
  Skip all user confirmation prompts.
- `--google-sheet`  
  List bridges in CSV format in Google Sheets.
- `--verbose`  
  Enable verbose output.

#### Notes:

- The ISO 8601 timestamp format is a standardized format for representing data and time information (Example: "2023-10-02T23:50:06.337+00:00")

#### Actions:

- If ESNs and start time are provided, it checks the preview recording status. If the `--google-sheet` option is provided, the status will be listed in Google Sheets.

## EXAMPLES

- To download a video from a camera:

```bash
een video download --esn 123456 --start-time "2024-10-01T00:00:00Z" --end-time "2024-10-01T01:00:00Z" --format mp4 --target-directory /path/to/save
```

- To list videos from a camera:

```bash
een video list --esn 123456 --start-time "2024-10-01T00:00:00Z" --end-time "2024-10-01T01:00:00Z" --verbose
```

- To check the status of a preview recording:

```bash
een video previewrecordingstatus --esns 123456 --start-time "2024-10-01T00:00:00Z" --end-time "2024-10-01T01:00:00Z" --verbose
```

# lpr - Manage License Plate Recognition (LPR) Events

## NAME

`lpr` - manage and retrieve License Plate Recognition events.

## SYNOPSIS

```
een lpr events [OPTIONS]
```

## DESCRIPTION

The `lpr events` command allows you to retrieve LPR events within a specified time frame. It supports filtering by license plate number and camera ID.

## COMMANDS

### events

Get License Plate Recognition events.

#### Required options:

- `--start-time [start time]`  
  Specify the start time for the events retrieval.

- `--end-time [end time]`  
  Specify the end time for the events retrieval.

#### Optional options:

- `--lp [license plate]`  
  Filter events by license plate number.

- `--esn [esn]`  
  Specify the camera ESN (Electronic Serial Number), which is the camera ID.

- `--verbose`  
  Enable verbose output.

- `--v3`  
  Use version 3 of the API for retrieving events.

#### Actions:

- If `--v3` is specified along with both `--start-time` and `--end-time`, it retrieves LPR events using version 3 of the API.
- If only the start and end times are specified, it retrieves LPR events using the default API.

## EXAMPLES

- To get LPR events for a specific time frame:

```bash
een lpr events --start-time "2024-10-01T00:00:00Z" --end-time "2024-10-01T23:59:59Z"
```

- To get LPR events for a specific license plate:

```bash
een lpr events --start-time "2024-10-01T00:00:00Z" --end-time "2024-10-01T23:59:59Z" --lp "ABC123"
```

# vsp - Manage Vehicle Surveillance Package (VSP) Events and Alerts

## NAME

`vsp` - manage and retrieve Vehicle Surveillance Processing events and alerts.

## SYNOPSIS

```
een vsp [COMMAND] [OPTIONS]
```

## DESCRIPTION

The `vsp` command allows you to manage and retrieve VSP events and alerts based on various parameters such as time, vehicle characteristics, and alert types.

## COMMANDS

### listevents

Get VSP events.

#### Options

- `--start-time [start time]`  
  Specify the start time for the events retrieval.

- `--end-time [end time]`  
  Specify the end time for the events retrieval.

- `--lp [lp]`  
  Filter events by license plate number.

- `--esns [esns]`  
  Specify camera ESNs (Electronic Serial Numbers).

- `--makes [makes]`  
  Filter by vehicle makes.

- `--locations [locations]`  
  Filter by location name.

- `--colors [colors]`  
  Filter by vehicle colors.

- `--body-types [types]`  
  Filter by vehicle body types.

- `--directions [directions]`  
  Specify the direction of the vehicle.

- `--access-type [access type]`  
  Specify the type of access.

- `--html`  
  Generate a chart in an HTML file.

- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.

- `--no-prompt`  
  Skip all user confirmation prompts.

- `--verbose`  
  Enable verbose output.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.

#### Actions:

- If `--html` is specified, it generates a report of VSP events.
- If not, it retrieves VSP events and saves them according to the specified options.

---

### listalerts

Get VSP alerts.

#### Options

- `--start-time [start time]`  
  Specify the start time for the alerts retrieval.

- `--end-time [end time]`  
  Specify the end time for the alerts retrieval.

- `--esns [esns]`  
  Specify the camera ESN (Electronic Serial Number).

- `--locations [locations]`  
  Specify the name of the location.

- `--allowed-vehicle`  
  Alert type: allowed vehicle.

- `--denied-vehicle`  
  Alert type: denied vehicle.

- `--count-of-license-plate`  
  Alert type: count of license plate.

- `--hotlist`  
  Alert type: hotlist.

- `--unregistered-vehicle`  
  Alert type: unregistered vehicle.

- `--watch-vehicle`  
  Alert type: watch vehicle.

- `--html`  
  Generate a chart in an HTML file.

- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.

- `--no-prompt`  
  Skip all user confirmation prompts.

- `--verbose`  
  Enable verbose output.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.

#### Actions:

- If `--html` is specified, it generates a report of VSP alerts.
- If not, it retrieves VSP alerts and saves them according to the specified options.

## EXAMPLES

- To get VSP events for a specific time frame:

```bash
een vsp listevents --start-time "2024-10-01T00:00:00Z" --end-time "2024-10-01T23:59:59Z"
```

- To get VSP alerts for allowed vehicles:

```bash
een vsp listalerts --start-time "2024-10-01T00:00:00Z" --end-time "2024-10-01T23:59:59Z" --allowed-vehicle
```

# pos - Manage Point of Sale (POS) Events

## NAME

`pos` - manage and retrieve Point of Sale events.

## SYNOPSIS

```
een pos listevents [OPTIONS]
```

## DESCRIPTION

The `pos` command allows you to manage and retrieve POS events based on various parameters such as time, transaction details, and location.

## COMMANDS

### listevents

Get POS events.

#### Options

- `--start-time [start time]`  
  Specify the start time for events retrieval.

- `--end-time [end time]`  
  Specify the end time for events retrieval.

- `--locations [locations]`  
  Specify the name of the location.

- `--transaction-type [transaction type]`  
  Specify the type of the transaction.

- `--net-amount-min [net amount min]`  
  Specify the minimum net amount.

- `--net-amount-max [net amount max]`  
  Specify the maximum net amount.

- `--employee-id [employee id]`  
  Specify the ID of the employee.

- `--discount-min [discount min]`  
  Specify the minimum discount in percentage.

- `--discount-max [discount max]`  
  Specify the maximum discount in percentage.

- `--bill-number [bill number]`  
  Specify the bill number.

- `--flagged`  
  Retrieve flagged transactions.

- `--html`  
  Generate a chart in an HTML file.

- `-f, --file-name [file name]`  
  Specify the name of the file where the output will be saved.

- `--no-prompt`  
  Skip all user confirmation prompts.

- `--verbose`  
  Enable verbose output.

#### Notes:

- If you haven't specified any start-time and end-time it will take last 24 hours as default timestamps.

#### Actions:

- If `--html` is specified, it generates a report of POS events.
- If not, it retrieves POS events and saves them according to the specified options.

## EXAMPLES

- To get POS events for a specific time frame:

```bash
een pos listevents --start-time "2024-10-01T00:00:00Z" --end-time "2024-10-01T23:59:59Z"
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

Update google config option values

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

#### Generate Credentials for accessing google sheets and google drive

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

#### Grant Editor permission to access google drive folder

Grant permission to your client email in your google drive folder.
Client email is the email that you get while initializing the project in google cloud console.

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

While executing google sheets commands, if you encounter any error messages like:

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

Replace these values with your credentials, you will be able to get the google sheets commands working.

#### To update the google config values, you can also use the command:

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
10. user-name - [Camera username]
11. password - [Camera password]
12. aspect-ratio- [Preview aspect ratio]
13. video-capture-mode - [Preview Record when]
14. preview-interval-ms - [Preview update rate]
15. preview-quality - [Preview quality]
16. preview-only-cloud-retention - [Cloud Preview Only (PR1)]
17. audio-enable - [Enable audio if available]
18. audio-disable - [Disable audio if available]

Note:

- Except for `cameraID` and `cameraName` all other field in camera settings file are editable.

### Bridge settings that can be edited:

1.local-rtsp-metrics - [Bridge rtsp metrics]

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
