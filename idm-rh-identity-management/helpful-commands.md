# Helpful Commands

## Validate idM Services

`ipactl status # run as root`

## Get Kerberos Ticket

`kinit admin`

## Validate Kerberos KDC

`klist`

View Replication via CLI \# Need to know Directory Manager password

**Domain**

`ipa-replica-manage list`

**CA**

`ipa-csreplica-manage list`

## Full list of ipa commands

`ipa help commands`

## List all HBAC rules

`ipa hbacrule-find --all`

## Show specific rule

`ipa hbacrule-show <rulename> --all`

OR

`ipa hbacrule-find --name=<rulename>--all`

## List all user logins

ipa user-find \| grep "login"

## Full info about a user

`ipa user-find --login=<login> --all`

## List all groups

`ipa group-find`

## Full info about a group

`ipa group-find --group-name=<group_name> –all`

## List allhostgroups

`ipa hostgroup-find`

## Full info about a hostgroup

`ipa hostgroup-find --hostgroup-name=<hostgroupname> --all`

## List DNS Zones

`ipa dnszone-find`

### `Set DNS Zones`

```text
ipa dnszone-add --name-from-ip=172.27.57.0/24 --allow-sync-ptr=true --default-ttl=60 --minimum=60
```

#### 

## List DNS records in a Zone

`ipa dnsrecord-find <DNS Zone>`

## Backup IDM

`ipa-backup`

## Set instance to create home directories for IDM users

`authconfig --enablemkhomedir --update`

## List sudo rules

`ipa sudorule-find`

## Show sudo Rule

`ipa sudorule-show <rule_name>`

