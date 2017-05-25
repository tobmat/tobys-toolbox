#### Design Considerations:

Database should be configured for high availability and disaster recovery

#### Helpful commands:

Check latency to database within region:

```
vmdb
rails runner tools/db_ping.rb
```

Check inter-region latency:

```
rails runner tools/db_ping_remote.rb
```

#### Helpful SQL commands:

Count of items on miq\_queue:  


```
select COUNT(*) from miq_queue;
```

Current items on the miq\_queue:

```
select id,priority,method_name,state,queue_name,zone,role,created_on,class_name from miq_queue;
```

Items on miq\_queue in error state:

```
select id,priority,method_name,state,queue_name,zone,role,created_on,class_name from miq_queue where state = 'error';
```

Get unique values from a field:

```
select distinct zone from miq_queue;
```

#### Delete appliance from a zone:

1. Navigate to Configure \| Configuration \| Diagnostics
2. Select the zone the server is in.
3. Select Configuration and Delete Server xxxxxxx



