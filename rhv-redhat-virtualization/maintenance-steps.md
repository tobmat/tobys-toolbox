# Maintenance Steps

#### Update RHV manager&#x20;

1. Global Maintenance Mode for RHV Manager &#x20;

From a host-&#x20;

hosted-engine --set-maintenance --mode=global &#x20;

1.  Update RHV Manager &#x20;

    engine-upgrade-check&#x20;

    yum update ovirt\\\*setup\\\*&#x20;

    engine-setup&#x20;

    yum update&#x20;
2. Remove RHV Manager from Global Maintenance Mode&#x20;

`hosted-engine --set-maintenance --mode=none `

1. Verify RHV Manager is online&#x20;

`hosted-engine --vm-status | egrep -i "engine status|hostname|cluster" `

If cluster is in maint mode the output of this command will have this line: \
`!! Cluster is in GLOBAL MAINTENANCE mode !! `

It should always have lines for each node with 2 of them with the status "vm not running on this host" and one with a status with health and should be good.&#x20;

1. Validate you can access RHV Web UI&#x20;

#### Update RHV Nodes&#x20;

1. Login to RHV Manager Web UI &#x20;
2. Click Hosts Tab&#x20;

Repeat following steps on all hosts&#x20;

1. Put Host in Maintenance Mode  (Right click on Host, Management, Maintenance)&#x20;
2. Wait for all VM's to migrate off (You can view status from UI Virtual Machines tab.  You have to scroll over to see the status column)&#x20;
3. Check for Updates (Hosts Tab) (Right click on Host, Installation, Check for Upgrade)&#x20;
4. Upgrade (Hosts Tab) (Right click on Host, Installation, Upgrade)&#x20;
5. Once the host is back online - Activate to remove from Maintenance Mode (Right click on Host, &#x20;

Management, Activate)&#x20;

#### RHV Manager DB Backup

```
/etc/crontab 

 

  30 3 * * * root /usr/local/bin/backup.sh >/dev/null 2>&1 
```

```
/usr/local/bin/backup.sh 

 

#!/bin/bash 
# 
# backup RHV manager 
# can be done nightly 
# 
# backup file location 

BKP_DIR="/opt/rhv_manager/backup" 

# backup file 

BKP_FILE="${BKP_DIR}/backup.$(/bin/date +%Y%m%d%H%M%S)" 

# make BKP_DIR in case it does not exist 

mkdir -p "${BKP_DIR}" 

# backup RHV manager 

/usr/bin/engine-backup --scope=all --mode=backup --log="${BKP_FILE}.out" --file="${BKP_FILE}.tar.gz" 
```

#### Troubleshooting&#x20;

From host:&#x20;

`nodectl check # status of the host `

`lvs -a | grep -e "^  pool00 " -e "Data%" | cut -c –135`   # This show how much space metadata pool is using.  This was a problem we encountered.  nodectl check also failed when this happened.  Resulted in rebuilding the host&#x20;

From rhv manager:&#x20;

Log file of messages displayed in ui:  /var/log/ovirt-engine/engine.log&#x20;

Collect Logs for redhat (from rhv manager): ovirt-log-collecter&#x20;

[https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/administration\_guide/sect-the\_log\_collector\_tool](https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/administration\_guide/sect-the\_log\_collector\_tool)&#x20;

#### Reference Links&#x20;

[https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/self-hosted\_engine\_guide/chap-maintenance\_and\_upgrading\_resources](https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/self-hosted\_engine\_guide/chap-maintenance\_and\_upgrading\_resources)&#x20;

[https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/upgrade\_guide/manually\_updating\_virtualization\_hosts](https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/upgrade\_guide/manually\_updating\_virtualization\_hosts)&#x20;

[https://access.redhat.com/solutions/444593](https://access.redhat.com/solutions/444593)&#x20;
