# NxPortalReports

## Features

### Web app

- Create & update reports
- View previously generated reports
- Enable/Disbale reports
- Send report now (sends the report instanly)
- Monitor system health
- Configure the tool

### Reports

- Content:
  - Add a first page (You can edit it using HTML)
  - Add as many dashboards as needed
  - (Pro tip): You can add pages to pdf by simply adding links to html pages
- Set period scope of dashboards linked (day/week/month/quarter)
- PDF page resolution (size) per report:
  - This will change how the dashboards are rendered (similar to resizing your browser)
- Email reports (support multiple emails and CCing)
- Customize the email template per report
- Schedule reports using cron-like scheduler
- Copy generated pdfs to an external directory (set COPY_DIR in config to a valid directory)

### Tool monitoring and status

- Status page:
  - Information on health of the system
  - Displays any problem in generation of a report
- Emailing:
  - Each day an email is sent with a list of problems in generating pdfs. (No email is sent if all is ok)

### One click installation on Nexthink Appliances

- Tool is packaged in an RPM and comes with an install script to install and configure database locally
- Tool is compiled with all of its dependencies to avoid problems

## Install

- [1.0.1 release files](https://transfer.nexthink.com/index.php/s/5kDUzs9N4FWHTmJ)
- [1.1.0 release files](https://transfer.nexthink.com/index.php/s/ezU4roxoRau48fd)
- Copy the `install-centos.sh` and the `rpm` to your machine
- Grant the install script execution permission: `$ sudo chmod +x install-centos.sh`
- Run the install script: `$ sudo ./install-centos.sh`
- Install the rpm: `$ sudo yum install nxPortalReports.rpm`

Note: recommended to install on Nexthink appliance. For other linux distributions contact me.
Note 2: In case you are using appliance 6.18+ make sure to check your hardening parameters. You might need to open port 5000 manually.

## Usage

- The server runs by default on port 5000
- Log in using admin / admin
- Go to settings page and configure your system.
- Go to reports page and start creating reports.

### Note

By deafult we parralelize up to 5 dashboard generations. You can change that by setting `PARALLEL_GENERATION` in the config (Check [config section](#Config)).
This will affect memory usage and speed/slow down the generation of reports.

### Config

#### If you need to change some configurations [optional]

Create a config module in `\var\nexthink\nxPortalReports\config\local.json`

A sample file is found in  `\var\nexthink\nxPortalReports\config\local.sample.json`

Make sure to restart the tool: `$ sudo systemctl restart nxPortalReports`

#### Current configs

- MONGO_URI
- WEB_APP_SERVER_PORT
- DEBUG
- BROWSER_PAGE_TIMEOUT
- ENCRYPTION_KEY
- PARALLEL_GENERATION
- COPY_DIR

#### sample

```json
{
  "MONGO_URI": "MONGODB URI",
  "WEB_APP_SERVER_PORT": 5000,
  "BROWSER_PAGE_TIMEOUT": 120000,
  "DEBUG": false,
  "ENCRYPTION_KEY": "32_CHARACTERS_PLEASE",
  "PARALLEL_GENERATION": 5,
  "COPY_DIR": null
}
```
```
