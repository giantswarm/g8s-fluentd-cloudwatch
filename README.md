# g8s-fluentd-cloudwatch
Fluentd cloudwatch helm recipe for g8s 

1. Download the helm chart

2. Configure the chart. 
  - Resources and limits can be tuned
  - Fluentd config can be changed too and provide a different one
  - Which aws region will receive the logs
  - Aws Role
  - Log group name in Cloud Watch

| Parameter                       | Description                                | Default                                                    |
| ------------------------------- | ------------------------------------------ | ---------------------------------------------------------- |
| `resources.limits.cpu`          | CPU limit                                  | `100m`                                                     |
| `resources.limits.memory`       | Memory limit                               | `200Mi`                                                    |
| `resources.requests.cpu`        | CPU request                                | `100m`                                                     |
| `resources.requests.memory`     | Memory request                             | `200Mi`                                                    |
| `awsRegion`                     | AWS Cloudwatch region                      | `us-east-1`                                                |
| `awsAccessKeyId`                | AWS access key id                          | `nil`                                                      |
| `awsSecretAccessKey`            | AWS secret access key                      | `nil`                                                      |
| `fluentdConfig`                 | Fluentd configuration                      | `example configuration`                                    |
| `logGroupName`                  | AWS Cloudwatch log group                   | `kubernetes`                                               |

3. Install the chart
```
helm install --name=fluentd ./ --set awsAccessKeyId=<AWS_ACCESS_ID> awsSecretAccessKey=<AWS_SECRET_KEY>
```

4. Check logs of fluentd pods. They should display messages like

```
[g8s-fluentd-cloudwatch-g2xhn] 2018-02-21 21:58:12 +0000 [info]: stats - namespace_cache_size: 1, pod_cache_size: 3, namespace_cache_api_updates: 3, pod_cache_api_updates: 3, id_cache_miss: 3
```

5. CLoudwatch logs should have now an entry called kubernetes with all streams from the k8s containers