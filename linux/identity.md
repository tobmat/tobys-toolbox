---
description: Linux identity components
---

# Identity

#### NSS - Name Service Switch - facility for common configuration&#x20;

/etc/nsswitch.conf - will have a sudo line if joined to IDM but not openldap

```
[root@tower01-prod ~]# grep sudoers /etc/nsswitch.conf
sudoers: files sss
```

#### sssd - System Security Services Daemon -&#x20;

/etc/sssd/sssd.conf - can determine what is being used for auth ( IDM or openldap for example)

#### Kerberos 5 auth

/etc/krb5.conf - \[realms] section shows what ldap service you are connected to

#### See all users

```
cat /etc/passwd
```
