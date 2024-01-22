# Introduction

## Latest CLI Version

The latest CLI release version: ![Latest Release](https://img.shields.io/github/v/release/EENCloud/EEN-CLI-Public)

## Environment variables

<a name="environment-variables"></a>

1. `API_KEY`

   - Creation: To get an `API_KEY` you will need an account. You can either use your existing account or create a Developer Account.

     - Existing account: You can create the key under your Account Settings.
     - Developer account: You will have to verify your email address first to create your Developer Account. Expect to get an email with a shortcut to create the `API_KEY`. Click on the shortcut link to create your `API_Key` and get started writing some code.

## Using the CLI

### Notes

- For all commands with `noprompt` option it will skip all user confirmation prompts. This means it will also overwrite any existing files without any confirmation.
- Open all the CSV file outputs in google sheet or libre office as excel has formatting issues.
- `verbose mode` : Use `--verbose` along with the commands to access the verbose mode.
- Supported `EEN TIME FORMATS` :
  - 20230125062511.000
  - 2023-01-31
  - 2023-01-31T08:24:32

## Setting-up of Executable File

- Extraction of file from a compressed file format
  #### **In Linux:**

  -  There are multiple ways to extract file from a compressed file here are the step by step instruction:

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
    v1.2.0 20231102
    Usage: een [command] options

    get version

    Options:
      -v, --version                              get current CLI version
      -h, --help                                 display help for command

    Commands:
      help
      auth
      location
      user
      account
      archive
      lpr
      bridge
      camera
      download
      update-google-config <optionName> <value>

    use een help command for detailed help instructions

    ```

### List of commands supported:

#### EEN Version

```
een --version
```

#### EEN Help

```
een help
```

Note: The `een help` command shows the detailed help instructions and
the help option `een <object> --help` shows the shorter version of help.

Examples:

- een help
- een --help
- een -h
- een auth --help
- een camera list --help

#### EEN account login

```
een auth login --username <username> --password <password> [--apikey <api key>]
```

Note: Password should be given in quotes, as the shell might have converting issues.

Example:

```
een auth login --username abc@een.com --password \***\*\*\*\*\***
```

To obtain the API_KEY, please see [here](#environment-variables)

#### EEN account status

```
een auth status --username <username> --password <password> [--apikey <api key>]
```

Example

```
een auth status --username abc@een.com --password \***\*\*\*\*\***
```

#### List bridges

```
een bridge list
```

#### List cameras

```
een camera list
```

#### List locations

```
een location list
```

#### List users

```
een user list
```

#### List bridges in CSV format

```
een bridge list --csv [-f/--filename <filename>] [--noprompt]
```

Fields in bridge csv: Bridge ID, Name, IP Address, Timezone, Serial Number, Location, GUID, Firmware Version

#### List cameras in CSV format

```
een camera list --csv [-f/--filename <filename>] [--noprompt]
```

Fields in camera csv: Camera ID, Bridge ID, Account ID, Name, IP Address, Timezone, Tags, Type, Service Status, Permissions, Serial Number, Timezone UTC Offset, Is Unsupported, Is Shared, Owner Account Name, Is UPNP, Video Input, Video Status, Location, Parent Camera ID, Child Camera View, Is Hidden, Ignored Inputs, Responder Camera, Discovered State, GUID, Duty Cycle, Camera Model, Cloud Retention, Local Retention Days, Video Resolution, MAC Address, Firmware Version

#### List cameras in CSV format with purging

```
een camera list --csv --purge -start_time [start_time] --end_time [end_time] [-f/--filename <filename>] [--noprompt]
```

Fields in camera csv: Camera ID, Bridge ID, Account ID, Name, IP Address, Timezone, Tags, Type, Service Status, Permissions, Serial Number, Timezone UTC Offset, Is Unsupported, Is Shared, Owner Account Name, Is UPNP, Video Input, Video Status, Location, Parent Camera ID, Child Camera View, Is Hidden, Ignored Inputs, Responder Camera, Discovered State, GUID, Duty Cycle, IsPurging, Camera Model, Cloud Retention, Local Retention Days, Video Resolution, MAC Address, Firmware Version

#### List users in CSV format

```
een user list --csv [-f/--filename <filename>] [--noprompt]
```

Fields in user csv: First Name, Last Name, Email, Last Login, Permissions

#### List locations in CSV format

```
een location list --csv [-f/--filename <filename>] [--noprompt]
```

Fields in location csv: Location ID, Location Name

#### List cameras based on specific tag

```
een camera list --tag <tag_name>
```

Example:

```
een camera list --tag lobby
```

#### List bridges based on specific location

```
een bridge list --location <location_name>
```

Example:

```
een bridge list --location austin
```

#### List cameras based on specific location

```
een camera list --location <location_name>
```

Example:

```
een camera list --location austin
```

#### List bridges based on specific tag

```
een bridge list --tag <tag_name>
```

Example:

```
een bridge list --tag lobby
```

#### List cameras based on specific status

```
een camera list --status <status>
```

Example:

```
een camera list --status "Camera on"
```

#### List bridges based on specific status

```
een bridge list --status <status>
```

Example:

```
een bridge list --status "Camera on"
```

#### List available cameras

```
een camera list --available
```

#### List available bridges

```
een bridge list --available
```

#### Get camera list in tree format

```
een camera list --tree
```

#### Get bridge list in tree format

```
een bridge list --tree
```

#### Write camera list to a csv file

```
een camera list --short -f/--filename <filename> [--noprompt]
```

#### Write camera settings to a csv file

```
een camera settings --csv [-f/--filename] [filename] [--noprompt]
```

#### Get camera status

```
een camera status
```

#### Get camera status in CSV format

```
een camera status --csv [-f/--filename <filename>] [--noprompt]
```

#### Get camera video list

```
een download list --esn <esn> --start_time <start_time> --end_time <end_time>
```

Example:

```
een download list --esn 1kj6eo83 --start_time 20220826084300.000 --end_time 20220826084330.000
```

#### Get camera video download

```
een download video --esn <esn> --start_time <start_time> --end_time <end_time> --format <format> --timestamp [timezone] --output <output> [--overwrite]
```

Note:

- For video download, we support both mp4 and flv format. We are writing the videos to the given output folder.
- The timestamp option is only supported for mp4 format
- Video download is done by batches of 5 videos at a time.

Example:

```
een download video --esn 1kj6eo83 --start_time 20220826084300.000 --end_time 20220826084330.000 --format mp4 --timestamp "US/Central" --output "foldername" --overwrite
```

#### Get LPR Events

```
een lpr events --start_time <start_time> --end_time <end_time> --lp <license plate> --esn <esn>
```

Example:

```
een lpr events --start_time 20221003183000.000 --end_time 20221004182959.000 --lp RJC9839 --esn 100d4of
```

#### Edit camera settings

```
een camera set <esn> --cloud_retention_days <cloud_retention_days> --video_resolution <video_resolution> [--noprompt]
```

Example:

```
een camera set 100jhi7 --cloud_retention_days 28 --video_resolution 3MP
```

#### Edit settings of all cameras

```
een camera set "*" --cloud_retention_days <cloud_retention_days> --video_resolution <video_resolution> [--noprompt]
```

Example:

```
een camera set "*" --cloud_retention_days 28 --video_resolution 3MP
```

Note: * Should be specified in quotes, as the shell might have converting issues.

#### Edit multiple camera settings

```
een camera bulk-set --esns <value1,value2> --cloud_retention_days <cloud_retention_days> --video_resolution <video_resolution> [--noprompt]
```

Example:

```
een camera bulk-set --esns 100ksh9,8991jgd --cloud_retention_days 30 --video_resolution 1080P
```

#### Edit camera settings based on tags

```
een camera tag-set --tag <tag> --cloud_retention_days <cloud_retention_days> --video_resolution <video_resolution> [--noprompt]
```

Example:

```
een camera tag-set --tag lobby --cloud_retention_days 28 --video_resolution 1080P
```

#### Edit multiple camera settings reading esn from csv file

We can execute the command een camera list --short to generate the csv file. This output csv file will act as the input for the below command.

```
een camera multi-set --cloud_retention_days <cloud_retention_days> --video_resolution <video_resolution> -f/--filename <filename> [--noprompt]
```

Example:

```
een camera multi-set --cloud_retention_days 30 --video_resolution 3MP --filename abc.csv
```

#### Edit multiple camera settings reading esn and camera settings from csv file

We can execute the command een camera settings to generate the csv file. This output csv file will act as the input for the below command.

```
een camera detailed-set -f/--filename <filename> [--noprompt]
```

Example:

```
een camera detailed-set -f abc.csv
```

#### Add camera to bridge

```
een camera add <esn> --camera_name <camera_name> --guid <guid> --location [location_id] --cloud_retention_days [cloud_retention_days] --scene [scene] --tags [tags] --username [username] --password [password] [--noprompt]
```

Example:

```
een camera add 1000red0 --camera_name "New Camera 5" --cloud_retention_days 30 --guid 5c445010-39f5-443e-8b0b-453119c5e062 --tags test
```

#### Delete camera from the bridge

```
een camera delete <esn>
```

Example:

```
een camera delete 1010red
```

#### Camera stream status csv

```
een camera streamstatus --esn [esn] --stream_type [stream_type] --start_time <start_time> --end_time <end_time> -f/--filename <filename> [--noprompt]
```

Example:

```
een camera streamstatus --esn 1010rbh --start_time 20230509062511.000 --end_time 20230509062611.000 --stream_type preview
```

Note:

- stream_type can be fullvideo or preview
- start_time can be "-1h" i.e., one hour before current time
- end_time can be "now" i.e., current time

#### List archives

```
een archive list
```

#### List archives detailed

```
een archive list --detailed
```

#### List archives in CSV format

```
een archive list --csv
```

#### List archives in a specific folder

```
een archive list --folder <folder>
```

Example:

```
een archive list --folder "snapshots/"
```

#### List archives in a specific folder detailed

```
een archive list --folder <folder> --detailed
```

Example:

```
een archive list --folder "snapshots/" --detailed
```

#### List archives in a specific folder in CSV format

```
een archive list --folder <folder> --csv
```

Example:

```
een archive list --folder "snapshots/" --csv
```

#### Archive download

```
een archive download <archive> --output <output> [--overwrite]
```

Example:

```
een archive download "snapshots/test-1.jpeg" --output "foldername" --overwrite
```

### For Generating HTML Reports

#### Bridge list report

```
een bridge list --html
```

#### Camera list report

```
een camera list --html
```

#### Bridge status report

```
een bridge status --html
```

#### Camera status report

```
een camera status --html
```

#### User permission report

```
een user list --html
```

### For Generating Lists In Google SpreadSheet

#### Bridge list

```
een bridge list --googleSheet
```

#### Camera list

```
een camera list --googleSheet
```

#### Camera list with purging

```
een camera list --googleSheet --purge -start_time [start_time] --end_time [end_time]
```

#### Bridge status list

```
een bridge status --googleSheet
```

#### Camera status list

```
een camera status --googleSheet
```

#### User permission list

```
een user list ---googleSheet
```

#### Get camera purge list

```
een camera purge-list -start_time [start_time] --end_time [end_time] [-f/--filename <filename>] [--noprompt]
```

Example:

```
een camera purge-list --start_time "20231128140000.000" --end_time "20231128141000.000" -f purge-list.csv
```

```
een camera purge-list
```
Note: If you haven't specify any start_time and end_time it will take last 24 hours as default timestamps.

#### EEN account Logout

```
een auth logout
```

### For Reseller Account

#### List accounts

```
een account list
```

Example:

```
een account list
```

#### Switch account to `END_USER`

```
een account switch --subaccount_id <subaccount_id>
```

Example:

```
een account switch --subaccount_id 00001106
```

#### Switch back to `RESELLER_ACCOUNT`

```
een account switch
```

Example:

```
een account switch
```

### Update Values in the Google Config File

```
een update-google-config <name> -- <value>
```

Example:

```
een update-config "driveFolderID" -- "1giou_ghlihbZyUpwCx"
```

### For Google Sheets commands

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
een update-google-config <name> -- <value>
```

Example:

```
een update-config "driveFolderID" -- "1giou_ghlihbZyUpwCx"
```

### Camera settings that can be edited:

1. cloud_retention_days - [Cloud retention]
2. video_resolution - [Video resolution]
3. bridge_target_days - [Local retention - Min]
4. local_retention_days - [Local retention - Max]
5. preview_resolution - [Preview resolution]
6. preview_transmit_mode - [Preview transmit mode]
7. video_transmit_mode - [Video transmit mode]
8. video_quality - [Full Video quality]
9. tags - [Tags]
10. username - [Camera username]
11. password - [Camera password]
12. aspect_ratio- [Preview aspect ratio]
13. video_capture_mode - [Preview Record when]
14. preview_interval_ms - [Preview update rate]
15. preview_quality - [Preview quality]

Note:

- Expect for `cameraID`, `cameraName`and `cloudPreviewOnly` all other field in camera settings file are editable.

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