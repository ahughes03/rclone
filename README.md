Rclone Steps to Automation

Terminal in your Mac

First group of commands creates folders for the scripts you'll be implementing
```
export EDITOR=nano
mkdir ~/Documents/computer/scripts/
mkdir ~/Documents/computer/scripts/rclone/
cd ~/Documents/computer/scripts/rclone/
```

Next command creates a script called "rclone" and enters edit mode
```
touch ~/Documents/computer/scripts/rclone/rclone
nano ~/Documents/computer/scripts/rclone/rclone
```

Copy and paste the following into the script
```
#!/bin/bash
#!/usr/local/bin/rclone
if pidof -o %PPID -x "rclone"; then
exit 1
fi
/usr/local/bin/rclone move seedbox:downloads/complete/ /Volumes/"Storage 2TB"/"Seedbox rclone"/ --drive-chunk-size 64M --buffer-size 256M --bwlimit 96000 --checkers 16 --transfers 8 --delete-empty-src-dirs --ignore-existing --exclude _unpack/** -u -v --log-file ~/Documents/computer/scripts/rclone/log/log-rotate.sh
exit
```
Save and exit the script using "Ctrl+X" then "Y"

Command to give your computer to automatically execute the script

`chmod a+x ~/Documents/computer/scripts/rclone/rclone`

Make a folder and script for a logging script, and enter edit mode
```
mkdir ~/Documents/computer/scripts/rclone/log
touch ~/Documents/computer/scripts/rclone/log/log-rotate.sh
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

`chmod a+x ~/Documents/computer/scripts/rclone/log/log-rotate.sh`

Time to set up the automation schedule

`crontab -e`

Paste the following into the editor
```
*/5 * * * * /bin/bash ~/Documents/computer/scripts/rclone/rclone
57 23 * * * /bin/bash ~/Documents/computer/scripts/rclone/log/log-rotate.sh
```

Save and exit the script using "Ctrl+X" then "Y"
