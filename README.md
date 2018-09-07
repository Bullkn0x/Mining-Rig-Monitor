# Mining-Rig-Monitor

In ethOS, we often run into a situation, where one or more gpus have crashed but mining continues without rebooting the system.

This script reboots the system if some gpu(s) crashes when ethOS is being used.

After 5 mins of boot, it starts checking for gpu crash using json api of ethosdistro.
If some gpu(s) doesn't work for 4 min, the system is restarted.


setup
=====

Usage
=====
1st optional argument: rig name shown in ***.ethosdistro.com
              Example: 2e15d2
2nd optional argument: json api in ethosdistro site
              Example: "http://xyz.ethosdistro.com/?json=yes"
These two arguments are required if there is some issue in accessing some files in "/var/run/ethos".

Debugging optional argument: If it is set to "-debug", it dumps running gpu and total gpu number.


sample usage:
   $ ./miner.py
or $ ./miner.py 2e15d2 "http://xyz.ethosdistro.com/?json=yes"

  (if you want to dump debug info)
or $ ./miner.py -debug
or $ ./miner.py -debug 2e15d2 "http://xyz.ethosdistro.com/?json=yes" (required in case of access problem in "/var/run/ethos")


Cronjob setup
=============
Open cronjob using "crontab -e" command.
Add following line at the end -
   @reboot /home/ethos/ethos_monitor/miner.py
or @reboot /home/ethos/ethos_monitor/miner.py 2e15d2 "http://xyz.ethosdistro.com/?json=yes"

Now, restart the system. The script will launch autometically at startup.


log file
========
/home/ethos/gpu_crash.log
