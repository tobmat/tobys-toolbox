# Tower Troubleshooting

**Jobs show up in UI with no status:**

From linux utility instance as ec2\_user:

`tower-cli job status [Job ID]`

`tower-cli job monitor [Job ID]`

`tower-cli list –status [Status listed from above command]`

`tower-cli job cancel [Job ID]`



**Review status of the cluster:**

`curl https://tower.genesyscloud.io/api/v2/ping/ | python -mjson.tool`

\# Note – Timestamp of each node should be within a few minutes of each other

`rabbitmqctl cluster_status`

`supervisorctl status`

\# if services are not all from the same time it could indicate an issue.  Restart services with following command on each node:

`ansible-tower-service restart`

`awx-managelist_instances`



**Remove old instance from rabbitmq:**

`rabbitmqctl forget_cluster_node 'rabbitmq@11.254.2.230'`
