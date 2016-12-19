# CrashPlan

### Info:

This template creates an instance of a headless backups server using Code 42's CrashPlan.

Reference Links:

* [Link to Code 42's support page on headless Crashplan servers](https://support.code42.com/CrashPlan/4/Configuring/Using_CrashPlan_On_A_Headless_Computer)
* [Link to base Docker image and instructions](https://github.com/JrCs/docker-crashplan)
* [Link to useful article for running dockerized CrashPlan on Synology NAS](https://miketabor.com/run-crashplan-docker-synology-nas/)
 
### Usage:

 Select Crashplan from the Rancher Catalog. 
 
 Click deploy.
 
 Do some trickery with Crashplan to authenticate the server with your Crashplan account. As noted in the Code 42
 document on a headless Crashplan server, you need to do some manipulations on your "Local Machine" - the machine
 you want backed up by your Crashplan Docker server - to configure the "Headless Crashplan" running on Rancher.
 
 1. On your Local Machine, make a backup of the current .ui_info config file located:
 ..* Linux: /var/crashplan/data/id/.ui_info
 ..* OSX: /Library/Application Support/CrashPlan/.ui_info
 ..* Windows: C:\ProgramData\CrashPlan\.ui_info
 2. Log into your Headless Crashplan container and display and copy the text of it's .ui_info located:
 ..* /var/crashplan/data/id/.ui_info
 3. Paste that text into the .ui_info file on your Local Machine.
 4. Update the Local Machine file by replacing the IP at the end of the first/only line (should be 0.0.0.0 or 127.0.0.1) in that file with the IP of your docker host.
 5. Start the Local Machine CrashPlan GUI, which will now be accessing the instance of Crashplan on the Headless Crashplan server.
 ..* If all is good, you should be prompted to log into your Crashplan account.
 ..* You don't want to adopt the location as a backup, so X out of that option
 ..* Go into settings and at least set a friendly name for this computer
 ..* In the settings, you might also want click into "Inbound backup..." drill down and get backup code for this Crashplan instance
 6. Close the Crashplan GUI.
 7. Restore the backup of the .ui_info file you made on the first step.
 8. Open up the Crashplan GUI - now back running on your local machine.
 
 You should now have the new computer available as a destination for backups of your Local Machine.
 
 Congratulations!
 
 
