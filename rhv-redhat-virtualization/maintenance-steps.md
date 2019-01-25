# Maintenance Steps

#### Update RHV manager 

1. Global Maintenance Mode for RHV Manager  

From a host- 

hosted-engine --set-maintenance --mode=global  

1. Update RHV Manager  

   engine-upgrade-check 

   yum update ovirt\\*setup\\* 

   engine-setup 

   yum update 

2. Remove RHV Manager from Global Maintenance Mode 

`hosted-engine --set-maintenance --mode=none` 

1. Verify RHV Manager is online 

`hosted-engine --vm-status | egrep -i "engine status|hostname|cluster"` 

If cluster is in maint mode the output of this command will have this line:   
`!! Cluster is in GLOBAL MAINTENANCE mode !!` 

It should always have lines for each node with 2 of them with the status "vm not running on this host" and one with a status with health and should be good. 

1. Validate you can access RHV Web UI 

#### Update RHV Nodes 

1. Login to RHV Manager Web UI  
2. Click Hosts Tab 

Repeat following steps on all hosts 

1. Put Host in Maintenance Mode  \(Right click on Host, Management, Maintenance\) 
2. Wait for all VM's to migrate off \(You can view status from UI Virtual Machines tab.  You have to scroll over to see the status column\) 
3. Check for Updates \(Hosts Tab\) \(Right click on Host, Installation, Check for Upgrade\) 
4. Upgrade \(Hosts Tab\) \(Right click on Host, Installation, Upgrade\) 
5. Once the host is back online - Activate to remove from Maintenance Mode \(Right click on Host,  

Management, Activate\) 

#### RHV Manager DB Backup

```text
/etc/crontab 

 

  30 3 * * * root /usr/local/bin/backup.sh >/dev/null 2>&1 
```

```text
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

#### Troubleshooting 

From host: 

`nodectl check # status of the host` 

`lvs -a | grep -e "^  pool00 " -e "Data%" | cut -c –135`   \# This show how much space metadata pool is using.  This was a problem we encountered.  nodectl check also failed when this happened.  Resulted in rebuilding the host 

From rhv manager: 

Log file of messages displayed in ui:  /var/log/ovirt-engine/engine.log 

Collect Logs for redhat \(from rhv manager\): ovirt-log-collecter 

[https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/administration\_guide/sect-the\_log\_collector\_tool](https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.1/html/administration_guide/sect-the_log_collector_tool) 

#### Reference Links 

[https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/self-hosted\_engine\_guide/chap-maintenance\_and\_upgrading\_resources](https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.1/html/self-hosted_engine_guide/chap-maintenance_and_upgrading_resources) 

[https://access.redhat.com/documentation/en-us/red\_hat\_virtualization/4.1/html/upgrade\_guide/manually\_updating\_virtualization\_hosts](https://access.redhat.com/documentation/en-us/red_hat_virtualization/4.1/html/upgrade_guide/manually_updating_virtualization_hosts) 

[https://access.redhat.com/solutions/444593](https://access.redhat.com/solutions/444593) 

