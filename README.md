# Route based on headers:

Use the header `SVC` to select the desired upstream server:
```
curl -H "SVC:svc02" 127.0.0.1:9001 # envoy
curl -H "SVC:svc02" 127.0.0.1:9002 # haproxy
curl -H "SVC:svc02" 127.0.0.1:9003 # nginx
```
Valid options for `SVC` are: `svc01` and `svc02`.

If no value for `SVC` is chosen, default routing occurs.
