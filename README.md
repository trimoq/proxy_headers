# Route based on headers:

Start with `docker-compose`: `docker compose up && docker compose down`.


## Explicit section
Use the header `SVC` to select the desired upstream server:
```
curl -H "SVC:svc02" 127.0.0.1:9001 # envoy
curl -H "SVC:svc02" 127.0.0.1:9002 # haproxy
curl -H "SVC:svc02" 127.0.0.1:9003 # nginx
```
Valid options for `SVC` are: `svc01` and `svc02`.
If no value for `SVC` is chosen, default routing occurs.


## Consistent hashing

Use the header `SVC` with any value to be routed to a backend using consistent hashing 
```
curl -H "SVC:a" 127.0.0.1:7001 # envoy
curl -H "SVC:b" 127.0.0.1:7001 # envoy

curl -H "SVC:a" 127.0.0.1:7002 # haproxy
curl -H "SVC:b" 127.0.0.1:7002 # haproxy

curl -H "SVC:a" 127.0.0.1:7003 # nginx
curl -H "SVC:b" 127.0.0.1:7003 # nginx

```

Note that hashing is consistent within each proxy (each proxy will route you to the same backend if you request it with the same header) but not the same for all proxies (nginx may route different than haproxy)