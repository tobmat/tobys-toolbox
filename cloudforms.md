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

#### Delete appliance from a zone:

1. Navigate to Configure \| Configuration \| Diagnostics
2. Select the zone the server is in.
3. Select Configuration and Delete Server xxxxxxx



