#### Design Considerations:

Database should be configured for high availability and disaster recovery

#### Helpful commands:

Check latency to database within region:

```
vmdb
rails runner tools/db_ping.rb
```

Check inter-region latency

```
rails runner tools/db_ping_remote.rb
```



