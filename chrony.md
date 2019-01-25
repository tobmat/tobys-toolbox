# Chrony

### Implementation of NTP that replaced ntpd in RHEL7.

## Helpful commands:

#### timedatectl

```text
timedatectl #provides status info about current time settings
timedatectl set-ntp true|false # enable / disable ntp
```

#### chronyc

```text
chronyc -a 'burst 4/4' # Issue these 2 commands to force time sync
chronyc -a makestep    #
chronyc sources        # gives info about current time servers being used, use -v for details about columns
chronyc sourcestats    # additional info about time servers, -v for details about columns
chronyc tracking       # detailed NTP specific info
```

## Helpful files:

#### /etc/chrony.conf - configuration file

```text
# ntp servers
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
server 2.pool.ntp.org iburst
#
keyfile /etc/chrony.keys

# Specify the key used as password for chronyc.
commandkey 1

# Enable kernel RTC synchronization.
rtcsync

# In first three updates step the system clock instead of slew
# if the adjustment is larger than 10 seconds.
makestep 10 3

# Record the rate at which the system clock gains/losses time.
driftfile /var/lib/chrony/drift

# Listen for commands only on localhost.
bindcmdaddress 127.0.0.1
bindcmdaddress ::1
```

#### Note - changes to config file require service to be restarted:

```text
systemctl restart chronyd
```

#### /var/lib/chrony/drift - record the rate at which system clocl gains/loses time.  Value set in config

```text
         -51.748801             0.422532
```

## Additional Info:

[Red Hat Chrony config details](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sect-Understanding_chrony_and-its_configuration.html)

