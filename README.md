# Sample of Load testing with K6

## Step to run
```
$docker-compose up -d
$docker-compose ps

    Name               Command           State            Ports
------------------------------------------------------------------------
k6_grafana_1    /run.sh                  Up       0.0.0.0:3000->3000/tcp
k6_influxdb_1   /entrypoint.sh influxd   Up       8086/tcp
k6_k6_1         k6                       Exit 0
```

## Start load testing
```
$docker-compose run k6 run scripts/sample.js

Creating k6_k6_run ... done

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: scripts/sample.js
     output: influxdb=http://influxdb:8086/k6 (http://influxdb:8086)

  scenarios: (100.00%) 1 scenario, 5 max VUs, 50s max duration (incl. graceful stop):
           * default: Up to 5 looping VUs for 20s over 3 stages (gracefulRampDown: 30s, gracefulStop: 30s)


running (20.4s), 0/5 VUs, 143 complete and 0 interrupted iterations
default ✓ [======================================] 0/5 VUs  20s

    ✓ status is 200

    checks.....................: 100.00% ✓ 143 ✗ 0
    data_received..............: 110 kB  5.4 kB/s
    data_sent..................: 15 kB   746 B/s
    http_req_blocked...........: avg=23.29ms  min=21.3µs   med=44.2µs   max=785.86ms p(90)=212.61µs p(95)=289.14µs
    http_req_connecting........: avg=7.32ms   min=0s       med=0s       max=217.31ms p(90)=0s       p(95)=0s
    http_req_duration..........: avg=227.68ms min=182.58ms med=225.07ms max=275.79ms p(90)=244.8ms  p(95)=250.06ms
    http_req_receiving.........: avg=342.26µs min=103.1µs  med=296.3µs  max=1.97ms   p(90)=510.54µs p(95)=692.06µs
    http_req_sending...........: avg=263.58µs min=90.2µs   med=217.1µs  max=1.5ms    p(90)=460.77µs p(95)=540.68µs
    http_req_tls_handshaking...: avg=15.05ms  min=0s       med=0s       max=460.21ms p(90)=0s       p(95)=0s
    http_req_waiting...........: avg=227.07ms min=182.22ms med=224.67ms max=275.13ms p(90)=244.29ms p(95)=249.5ms
    http_reqs..................: 143     6.993068/s
    iteration_duration.........: avg=553.04ms min=516.3ms  med=527.81ms max=1.3s     p(90)=547.22ms p(95)=565.84ms
    iterations.................: 143     6.993068/s
    vus........................: 1       min=1 max=5
    vus_max....................: 5       min=5 max=5
```