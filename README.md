# NJ MVC Watch
```
Date: 2021-05-23
Author: Ghosal, Rahul D.
```
## I. Purpose
`njmvc_checker` was developed to automate the process of checking the the New Jersey Motor Vehicles Commission's (NJ MVC) appointment registration portal for availability in designated cities.

## II. Design
This package achieves its purpose by:
1. Receiving an input of (1) A desigated NJ MVC service (e.g., Initial Permits) and (2) A list of cities.
> *NOTE* : Currently, the scope of this program is limited to "initial permit" and "knowledge test."
2. Navigating to the webpage associated with (1).
3. Scraping the webpage for a target HTML element associated with each city within (2) that would indicate appointment availability.
4. E-mail designated addresses when appointments are available. This e-mail includes the list of cities (among those specified in (2)) where appointments are available and a link to the webpage.

## III. Usage
### 1. Setup
```bash
# Install Python, Chrome and chromedriver, as well as Linux utilites (e.g., wget, cron, etc.).
chmod +x init.sh
./init.sh 

# Edit and save environmental variables (DO NOT commit).
# See local.env_example for example.
vi local.env

# Install Python dependencies.
pip intall -r requirements.txt

```
>*NOTE*: Only GMail addresses are supported. Prior execution, **GMail must be set for two-step authentication and `GM_PWD` should be an Application password** generated by GMail. For more info, see: https://support.google.com/accounts/answer/185833?hl=en

***
### 2a. Execute as standalone script
```bash
# Load environmental variables and execute.
# Applicable services are either "knowledge test" or "initial permit."
source local.env
python3 -s <service_name> -c <comma-separated list of cities>
```
***
### 2b. Execute as cron job
```bash
# Configure crontab using a textfile to execute entrypoint.sh at a given time/interval.
crontab njmvc_cron.txt
```

## IV. Example Usage
Currently, the author runs this script every hour, at the 30-minute mark on an Ubuntu VPS via cron. See `njmvc_cron.txt` for sample. Execution also tested successfully on Docker (Ubuntu image), so package may be deployed as a container as well (see `test.Dockerfile` for informal example of build).

