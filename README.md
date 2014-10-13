openwrt-couchpotato
===================

Using Couchpotato on OpenWRT

Here are some thoughts around using Couchpotato on OpenWRT.
I installed python and git and Couchpotato seems to work fine, despite eating m a lot of my router's CPU.

Here is the init script I came up with. Quick and dirty approach...
/etc/init.d/couchpotato

#!/bin/sh /etc/rc.common

START=97

start() {
        #sleep 5
         #. /etc/profile
         #echo $PATH
        /usr/bin/python /root/scripts/CouchPotatoServer/CouchPotato.py --quiet --daemon --pid_file=/tmp/couchpotato.pid --data_dir=/root/.couchpotato
        # commands to launch application
}

stop() {
kill -9 $(cat /tmp/couchpotato.pid)
kill -9 $(ps |grep Couch | awk '{print $1}' |head -n 1)
rm /tmp/couchpotato.pid
}
