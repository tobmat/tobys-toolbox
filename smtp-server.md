# Troubleshooting:

Review /var/log/maillog on smtp server



If having relay issues verify relay is setup from IP you are coming from:

`cat /etc/mail/access`



**To add a relay:**

`vi /etc/mail/access`

1. Insert new relay line with 1st-3 octets of IP \(see other lines for examples\)

2. Restart sendmail service

`servicesendmailstatus`

`servicesendmailrestart`

`servicesendmailstatus`

