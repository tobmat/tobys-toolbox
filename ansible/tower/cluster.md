# cluster

[https://docs.ansible.com/ansible-tower/3.2.6/html/administration/proxy-support.html\#proxy-support](https://docs.ansible.com/ansible-tower/3.2.6/html/administration/proxy-support.html#proxy-support)

Use settings api to change - see api page

## Use tower-cli to change:

`tower-cli setting modify WEBSOCKET_ORIGIN_WHITELIST '[`

`"https://tower-eus.idm.us.int.genesyscloud.io",`

`"https://tower-eus.hub.genesyscloud.io"`

`]'`

`tower-cli setting modify REMOTE_HOST_HEADERS '[`

`"HTTP_X_FORWARDED_FOR",`

`"REMOTE_ADDR",`

`"REMOTE_HOST"`

`]'`

