# novdevops2021
This is november 2021 batch training repository
staledockerfolder.sh

#!/bin/bash

#*****************************************************************************************
# Script removes all stale directories of stopped or exited containers from /var/log/obs
#
#
#*****************************************************************************************

Now_daily=$(date +%d-%b-%Y)
sudo docker ps -q > /tmp/container_id_$Now_daily.txt
find /var/log/obs/ -name '*_*' -type d|
     grep -v -f /tmp/container_id_$Now_daily.txt >/tmp/delete_folder.txt
while read line
do
 sudo rm -rf $line
done </tmp/delete_folder.txt
