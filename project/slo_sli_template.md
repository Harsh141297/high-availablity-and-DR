# API Service

| Category     | SLI                                                                                                               | SLO                                                                                                         |
|--------------|-------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| Availability | Percentage of successful requests over the last 5 minutes                                                        | 99% of health-check responses should be successful                                                           |
| Latency      | 90% of requests finish in these times                                                                             | 90% of requests should have a response time below 100ms                                                       |
| Error Budget | Percentage of successful requests (Assuming code 200 as success)                                                  | Error budget is defined at 20%. This means that the error rate should not exceed 20% of total requests      |
| Throughput   | Successful requests per second                                                                                    | 5 RPS indicates the application is functioning                                                              |
