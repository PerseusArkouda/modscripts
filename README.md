# modscripts

### Scripts to manage Steam's workshop mods from Linux console. 
+ moddownloader and modunpacker can run independently.
+ modchecker requires both of the above.
+ You can either run with arguments: ./scriptname appid modid1 modid2 modid3 (etc...) or by setting up mods.conf.
+ Errors are both printed in console and logged in logs dir.

(Read inside the scripts for more info)



#### moddownloader 
+ Script to download/validate mods directly from Steam's workshop with steamcmd.
   Will resume if download is interrupted until it succeeds (max limit 30 attempts).
+ Requires steamcmd.

#### modunpacker 
+ Script to install directly downloaded mods from Steam's workshop to the game.
   Uses modified code from ark_update.sh: https://github.com/Nexolight/ark_xposed

#### modchecker
+ This script can be scheduled to run daily (or whatever) and validate all defined mods.
   Then it will verify if the downloaded mods (after validation) contain updates and it will update if needed.
   Example for crontab: @daily /path/to/modchecker
+ In case you want to use it for different sets of mods or server clusters, just rename the modscript folder and setup
   a different mods.conf with the other server paths and mod IDs. Make sure to set a good time apart in schedule because
   steamcmd won't let it run a new process while the previous one still running.
+ Requires both moddownloader and modunpacker scripts to work.
