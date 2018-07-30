Sorry I screwed up that log location command, which will in turn jack out the log rotation. Run these commands to fix:

We're going to edit the rclone script first

```
nano ~/Documents/computer/scripts/rclone/rclone
```

change the long command line from:

```
--log-file ~/Documents/computer/scripts/rclone/log/log-rotate.sh
```

to

```
--log-file ~/Documents/computer/scripts/rclone/log/rclone-cron.log
```

```
sudo rm ~/Documents/computer/scripts/rclone/log/log-rotate.sh
nano ~/Documents/computer/scripts/rclone/log/log-rotate.sh
```

Copy and paste the following into the script

```
#!/bin/bash
logdir='~/Documents/computer/scripts/rclone/log/'
cd $logdir
/usr/bin/test -f rclone-cron.log.7 && /bin/rm rclone-cron.log.7
/usr/bin/test -f rclone-cron.log.6 && /bin/mv rclone-cron.log.6 rclone-cron.log.7
/usr/bin/test -f rclone-cron.log.5 && /bin/mv rclone-cron.log.5 rclone-cron.log.6
/usr/bin/test -f rclone-cron.log.4 && /bin/mv rclone-cron.log.4 rclone-cron.log.5
/usr/bin/test -f rclone-cron.log.3 && /bin/mv rclone-cron.log.3 rclone-cron.log.4
/usr/bin/test -f rclone-cron.log.2 && /bin/mv rclone-cron.log.2 rclone-cron.log.3
/usr/bin/test -f rclone-cron.log.1 && /bin/mv rclone-cron.log.1 rclone-cron.log.2
/usr/bin/test -f rclone-cron.log && /bin/mv rclone-cron.log rclone-cron.log.1
```

Save and exit the script using "Ctrl+X" then "Y"

Command to give your computer to automatically execute the script

```
chmod a+x ~/Documents/computer/scripts/rclone/log/log-rotate.sh
```
