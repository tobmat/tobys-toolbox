# api

## System settings:

[https://\<host>/api/v2/settings/system/](https://\<host>/api/v2/settings/system/)

## Get auth token:

`curl -v -f -k -H 'Content-Type: application/json' -XPOST -d @tower_auth.txt https://towertest-eus.hub.genesyscloud.io/api/v2/authtoken/`

where @tower\_auth.txt contents are:

{"username": "username", "password": "password"}

### Update Ldap configuration

You can pull the LDAP settings directly from the api at `/api/v2/settings/ldap/`. In this view, the password and other secrets in the config will show as $encrypted$. You can copy that API output and replace the encrypted details with your secrets/passwords and post with a PUT call at the same endpoint. This will replicate over the same settings as the expected JSON will be exactly the same. This can also be done directly in your web browser using our browsable API implementation.  Note - You must remove the portion of the output at the bottom that has never been updated.  You just want to post the main ldap section.
