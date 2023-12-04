## Availability SLI
### The percentage of successful requests over the last 5m

rate(prometheus_http_requests_total[5m])



## Latency SLI
### 90% of requests finish in these times
histogram_quantile(0.9, sum(rate(prometheus_http_request_duration_seconds_bucket[5m])) by (le))


## Throughput
### Successful requests per second
rate(prometheus_http_requests_total[5m])


## Error Budget - Remaining Error Budget
### The error budget is 20%
sum(rate(prometheus_http_requests_total{status=~"5.."}[5m])) / sum(rate(prometheus_http_requests_total[5m])) * 100

