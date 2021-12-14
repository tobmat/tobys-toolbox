---
description: Notes about available linux command line utilities
---

# Command Line

#### id \<username> - displays all the groups associated with a user. (refreshes when a user logs into a system)

```bash
toby.matherly CORP-L-66FJG5J -> id toby.matherly
uid=503(toby.matherly) gid=20(staff) groups=20(staff),0(wheel),
12(everyone),61(localaccounts),79(_appserverusr),80(admin),81(_appserveradm)
```

#### getent - get entries from Name Service Switch libraries

```bash
# get list of users from a given group
getent group ae-users

# List all users managed by open ldap or local on given server 
# Doesn’t show idm managed users
getent passwd
```

#### check users sudo access

```bash
sudo -l -U toby.matherly
```

#### sss\_cache - Invalidate cached entries

```bash
sss_cache -E   # Invalidate ALL cached entries, forces refresh from IDM

sss_cache -u <user>   # Invalidate for specific user, forces refresh from IDM
```

#### Get octal permissions

```
stat -c '%A %a %n' filename
```
