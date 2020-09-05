# modscripts

### Scripts to manage Steam's workshop mods from Linux console. 
+ moddownloader and modunpacker can run independently.  
*modfunctions must be present as it holds shared functions for all the scripts.*
+ modchecker requires both of the above.
+ You can either run with arguments: ./scriptname appid modid1 modid2 modid3 (etc...) or by setting up mods.conf.
+ If you use them without mods.conf, define the correct path variables at the top of the scripts.
+ Errors are both printed in console and logged in logs dir.

(Read inside the scripts for more info)



#### moddownloader 
+ Script to download/validate mods directly from Steam's workshop with steamcmd.
   Will resume if download is interrupted until it succeeds (max limit 30 attempts).
+ Requires steamcmd.

#### modunpacker 
+ Script to install directly downloaded mods from Steam's workshop to the game.
+ Uses modified code from ark_update.sh: https://github.com/Nexolight/ark_xposed

#### modchecker
+ This script can be scheduled to run daily (or whatever) and validate all defined mods.
   Then it will verify if the downloaded mods (after validation) contain updates and it will update if needed.
+ Example for crontab: @daily /path/to/modchecker
+ In case you want to use it for different sets of mods or server clusters, just rename the modscript folder and setup
   a different mods.conf with the other server paths and mod IDs. Make sure to set a good time apart in schedule because
   steamcmd won't let it run a new process while the previous one still running.
+ It will install all defined mods automatically.
+ Requires both moddownloader and modunpacker scripts to work.

#### modfunctions
+ This script is not meant to be used directly.
+ Contains shared functions for the rest of the scripts.


### Purpose of these scripts
Some may wonder what's the reason of these scripts while there are others that do more.
The answer is quite simple: these do less by design.
I'm writing or adopting code from others for the scripts primarily to use myself and I have found
while some programs do more, it's more difficult for me to use them because I have already my personal
settings where those programs require from me to change. So my scripts offer that freedom (as much as possible)
to the user to not require to change his settings in order to use them and instead to customize them for a specific usage.
+ If you want just to download mod(s) you can do: ./moddownloader appid modid1 modid2
+ If you want just to install mod(s) you can do: ./modunpacker appid modid1 modid2
+ If you want to download/install a standard set of mods, then you can create and setup mods.conf
+ If you want to maintain a custom set of mods updated, then you can schedule to run modchecker from a scheduler like crontab
for example: @daily /path/to/modchecker appid modid1 modid2
+ If you want to maintain your standard set of mods updated, then you can create and setup mods.conf and schedule to run
modchecker from a scheduler like crontab

###### Note1: Even if you do have mods.conf the arguments are prioritized and override mods.conf's appid and modid(s) respectively.
###### Note2: If you don't use mods.conf you have to open the script you want to use individually and edit your path variables at the top.
