# Tower Troubleshooting

## Non-supported Database version

**Issue:** Error when attempting backup  setup.sh -b&#x20;

**Error:** "stderr": "pg\_dump: server version: 10.5; pg\_dump version: 9.6.11\npg\_dump: aborting because of server version mismatch"

**Problem:**  I installed non-supported version of postgres.  Tower worked but that backup functionality didn't.

**Solution:**  (Since you can't do a backup you can use these  commands to dump configuration.  Note - secrets, passwords, ssh keys will not be in the output and need to be re-added manually.)

```
tower-cli receive --all > tower-backup-20190123.json  # export tower configuration
tower-cli receive --credential all > tower-bu-creds.json #export all credentials
# Delete external DB
# Rebuild external DB
./setup # run tower setup to connect to new DB
# apply license
tower-cli send tower-bu-creds.json -v # restore the credentials
# manually add secrets, passwords, ssh-keys back to credentials
tower-cli send tower-backup-20190123.json -v # restore the remaining components
./setup -b # Validate ability to do backup
```

## **Jobs show up in UI with no status:**

From linux utility instance as ec2\_user:

`tower-cli job status [Job ID]`

`tower-cli job monitor [Job ID]`

`tower-cli list –status [Status listed from above command]`

`tower-cli job cancel [Job ID]`

## **Review status of the cluster:**

`curl https://tower.genesyscloud.io/api/v2/ping/ | python -m json.tool`

\# Note – Timestamp of each node should be within a few minutes of each other

`rabbitmqctl cluster_status`

`supervisorctl status`

\# if services are not all from the same time it could indicate an issue. Restart services with following command on each node:

ansible-tower-service`restart`

`awx-manage list_instances`

## **Remove old instance from rabbitmq:**

`rabbitmqctl forget_cluster_node 'rabbitmq@11.254.2.230'`

rabbitmqctl cluster\_status

## Reinstall Tower:

1. yum remove ansible-tower\*
2. On all nodes: rm -rf /var/lib/awx/venv/\*
3. ./setup.sh
