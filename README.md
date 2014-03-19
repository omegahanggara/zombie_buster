# Zombie Buster

### What is Zombie Buster?
Zombie buster is simple bash script to monitoring your proscesses, then killing zombie proscess when it found immediately. This scripts are very useful if you're using ROM based on JB 4.3, when it has annoying bug. The bug is, your system will spawn another system_server PID, where system_server should spawn once every boot, and one system_server is just enough. But in this case, somehow system_server will be spawned and multiple itself, which make your system become unresponsive, because your available memory consumed by those system_server-es.

### What do you need?
System requirements
  * Busybox-ed ROM
  * ROOT-ed ROM
  * ROM that support init.d

### How does it works?
These scripts has its own job. First **find_zombie** will watching your system process, and logging the result to ```/data/find_zombie.log```.  Second script is **trigger_zb**, this script will watching ```/data/find_zombie.log```, when zombie process(es) has found, it will tell the main script to kill them. Last script is **zombie_killer**, this scipt won't execute any command untill **trigger_zb** tell it that zombie process has found and need to be killed.

### How to install Zombie Buster?
Place every scripts to its place.
  * ./system/xbin/find_zombie -> /system/xbin/find_zombie
  * ./system/xbin/trigger_zb -> /system/xbin/trigger_zb
  * ./system/xbin/zombie_killer -> /system/xbin/zombie_killer
  * ./system/etc/init.d/90zombie_buster -> /system/etc/init.d/90zombie_buster

You can use adb to install these scripts
```
$ adb root
$ adb remount
$ adb push ./system/xbin/find_zombie /system/xbin/find_zombie
$ adb push ./system/xbin/trigger_zb /system/xbin/trigger_zb
$ adb push ./system/xbin/zombie_killer /system/xbin/zombie_killer
$ adb push ./system/etc/init.d/90zombie_buster /system/etc/init.d/90zombie_buster
```

After pushing those scripts, make sure you have set the permission
```
$ adb shell
shell@android:/$ su
root@android:/# chmod 755 /system/xbin/find_zombie
root@android:/# chmod 755 /system/xbin/trigger_zb
root@android:/# chmod 755 /system/xbin/zombie_killer
root@android:/# chmod 755 /system/etc/init.d/90zombie_buster
root@android:/# exit
shell@android:/$ exit
$
```

Reboot your phone. And DONE!
