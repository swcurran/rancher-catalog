# CrashPlan

### Info:

This template creates an instance of a headless backups server using Code 42's CrashPlan.

Reference Links:

* [Link to Code 42's support page on headless Crashplan servers](https://support.code42.com/CrashPlan/4/Configuring/Using_CrashPlan_On_A_Headless_Computer)
* [Link to base Docker image and instructions](https://github.com/JrCs/docker-crashplan)
* [Link to useful article for running dockerized CrashPlan on Synology NAS](https://miketabor.com/run-crashplan-docker-synology-nas/)
 
### Usage:

 Select Crashplan from the catalog. 
 
 Enter the IP of your Rancher Host and Crashplan port. This is necessary because by default the
 Crashplan server will use the IP of the container as the address of the server - and that will be unreachable.
 Let me know if there is a better way to set an environment variable in the docker-compose.yml
 with the docker host ip.  It's harder than I thought...
 
 Click deploy.
 
 Do some trickery with Crashplan to authenticate the server with your Crashplan account.
 
 * On your Crashplan Desktop machine, make a backup of the current .ui_info config file located:
 ..* Linux: /var/crashplan/data/id/.ui_info
 ..* OSX: /Library/Application Support/CrashPlan/.ui_info
 ..* Windows: C:\ProgramData\CrashPlan\.ui_info
 * Log into your new Crashplan container display and copy the text of it's .ui_info located:
 ..* /var/crashplan/data/id/.ui_info
 * Paste that text into the .ui_info file on your Desktop machine.
 * Update that file and replace IP (should be 0.0.0.0 or 127.0.0.1) at the end of the first line in that file with the IP of your docker host.
 * Start your local CrashPlan GUI - you should be prompted to log into your Crashplan account.
 * You should see your docker host as a backup target.
 
 
 
 
