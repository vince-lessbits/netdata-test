# Longish chart names will break streaming in v1.21 and greater

```
docker-compose up -d
```

In another terminal, watch the logs
```
docker-compose logs -f 
```

Navigate to the master in a browser at http://localhost:19999 and verify the
slave is replicating.

Exec into the slave and send in a loong statsd timer name:
```
docker-compose exec netdata-slave bash
printf "this-is-a.long_statsd_timer_name.to_simulate_programmatically_generated_names_from_mod_paths:1.0|ms\n" | nc -u -w 0 localhost 8125
```

View replication thrashing in the logs.

Stop the test:
```
docker-compose down
```
