---
description: General Notes on SNMP
---

# SNMP

```
# Status 
service snmpd status

# Start
service snmpd start

# Confirm snmpd set to auto-start on boot
chkconfig --list | grep snmpd
    
# Add to chkconfig (set to start on os startup or reboot)
chkconfig snmpd on
```
