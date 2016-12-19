# CrashPlan

### Info:

This template creates an instance of a headless backups server using Code 42's CrashPlan.

Reference Links:

* [Link to Code 42's support page on headless Crashplan servers](https://support.code42.com/CrashPlan/4/Configuring/Using_CrashPlan_On_A_Headless_Computer)
* [Link to base Docker image and instructions](https://github.com/JrCs/docker-crashplan)
* [Link to useful article for running dockerized CrashPlan on Synology NAS](https://miketabor.com/run-crashplan-docker-synology-nas/)
 
### Usage:

 Select Crashplan from the catalog. 
 
 Click deploy.
 
 Do some trickery with Crashplan to authenticate the server with your Crashplan account. As noted in the Code 42
 document on a headless Crashplan server, you need to do some manipulations on your "Local Machine" - the machine
 you want backed up by your Crashplan Docker server and the "Headless Crashplan" running on Rancher.
 
 1. On your Local Machine, make a backup of the current .ui_info config file located:
 ..* Linux: /var/crashplan/data/id/.ui_info
 ..* OSX: /Library/Application Support/CrashPlan/.ui_info
 ..* Windows: C:\ProgramData\CrashPlan\.ui_info
 2. Log into your Headless Crashplan container and display and copy the text of it's .ui_info located:
 ..* /var/crashplan/data/id/.ui_info
 3. Paste that text into the .ui_info file on your Desktop machine.
 4. Update that file and replace IP (should be 0.0.0.0 or 127.0.0.1) at the end of the first line in that file with the IP of your docker host.
 5. Start your local CrashPlan GUI, which will now be access the instance of Crashplan on the Docker container.
 ..* If all is good, you should be prompted to log into your Crashplan account.
 ..* You don't want to adopt the location as a backup, so X out of that option
 ..* Go into settings and at least set a friendly name for this computer
 ..* In the settings, you might also want click into "Inbound backup..." drill down and get backup code for this Crashplan instance
 6. Close the Crashplan GUI.
 7. Restore the backup of the .ui_info file you made on the first step.
 8. Open up the Crashplan GUI - now back running on your local machine.
 
 Set the internal IP address of Crashplan to the Rancher Host IP
 
 1. Log into your Headless Crashplan container (open a Shell)
 2. Go to: /var/crashplan/data/conf
 3. Edit the file .ui_properties and:
 ..* Uncomment the "ServiceName" line
 ..* Set the IP address on that line to the IP of your Docker Host
 4. Restart the Crashplan container
 5. Restart the Crashplan GUI on your local machine and verify that the internal address of your Rancher backup 
 
 
 
 
