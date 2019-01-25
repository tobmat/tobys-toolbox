# Cloudforms

## Design Considerations:

### Database should be configured for high availability and disaster recovery

## Helpful commands:

### Check latency to database within region:

```text
vmdb
rails runner tools/db_ping.rb
```

### Check inter-region latency:

```text
vmdb
rails runner tools/db_ping_remote.rb
```

## Helpful SQL commands:

### Enter Rails db session to enter SQL commands:

```text
vmdb
rails db  # This will require password
```

### Count of items on miq\_queue:

```text
select COUNT(*) from miq_queue;
```

### Current items on the miq\_queue:

```text
select id,priority,method_name,state,queue_name,zone,role,created_on,class_name from miq_queue;
```

### Items on miq\_queue in error state:

```text
select id,priority,method_name,state,queue_name,zone,role,created_on,class_name from miq_queue where state = 'error';
```

### Get entries prior to x date:

```text
select * from miq_queue where created_on < '2016-12-31';
```

### Get unique values from a field:

```text
select distinct zone from miq_queue;
```

## Delete appliance from a zone:

1. Navigate to Configure \| Configuration \| Diagnostics
2. Select the zone the server is in.
3. Select Configuration and Delete Server xxxxxxx

```text
Note - This is actually doing a destroy which can take a really long time due to deleting all events 
associated with an appliance.  To delete only the server out of the DB you can issue this command:

MiqServer.where(:id=> 100000000000002).take.delete
```

## Test DB Latency:

```text
vmdb
rails runner tools/db_ping.rb
```

## Rake commands:

```text
vmdb
rake --tasks evm    # list all available rake tasks in evm namespace
rake --tasks atg    # list all custom rake tasks in atg namespace
rake --tasks        # list all available rake tasks
rake evm:status     # Report status of ManageIQ EVM application
```

API info:

```text
'r' is shorthand for all 0's in a number.  For example 100000000000007 can be referred to as 1r7 
in scripting or API calls.
```

