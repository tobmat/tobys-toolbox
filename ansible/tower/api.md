#### System settings:

[https://&lt;host&gt;/api/v2/settings/system/](https://<host>/api/v2/settings/system/)

#### Get auth token:

`curl -v -f -k -H 'Content-Type: application/json' -XPOST -d @tower_auth.txt https://towertest-eus.hub.genesyscloud.io/api/v2/authtoken/`

where @tower\_auth.txt contents are:

{"username": "username", "password": "password"}

