# Tower

## Import existing inventories / variables into tower

* see tips and tricks below
* create empty inventory in tower
* On tower server copy an existing inventory structure in inventory/ directory
* execute this command:

```text
tower-manage inventory_import --source=inventory/ --inventory-name="<inventory name>"
```

## AD Setup

Test from server --

`ldapsearch -x -H ldap://WIN-REURSSQETGV -D "CN=atgservice,OU=Users,OU=pureconnect,DC=pureconnect,DC=cloud" -b "dc=pureconnect,dc=cloud" -w <userpassword>`

## Tips and Tricks

[http://docs.ansible.com/ansible-tower/latest/html/administration/tipsandtricks.html](http://docs.ansible.com/ansible-tower/latest/html/administration/tipsandtricks.html)

## Tower Server

/var/lib/awx/projects - where playbooks are stored

/etc/tower/conf.d - some configuration settings files

ansible-tower-service - tower service

/etc/openldap/certs/ - location for your wildcard certs

/var/lib/pgsql - location of database if local

