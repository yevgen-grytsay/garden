---
{"dg-publish":true,"permalink":"/open-telemetry-log-record-transformer/","tags":["otel","open-telemetry","otel-collector","logs"]}
---



[proto.LogRecord](https://github.com/open-telemetry/opentelemetry-proto/blob/main/opentelemetry/proto/logs/v1/logs.proto#L134)
[Log Context](https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/pkg/ottl/contexts/ottllog)
[transform processor Troubleshooting](https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/transformprocessor/README.md#troubleshooting)
## Приклад додавання атрибута
Беремо значення `level` із об'єкта `body` і створюємо з цим значенням новий атрибут `level`.
```yaml
config:
  processors:
    transform:
      log_statements:
        - context: log
          conditions:
            - IsMap(body) and body["level"] != nil
          statements:
            - set(attributes["level"], body["level"])
```

```json
{
  "kind": "processor",
  "name": "transform",
  "pipeline": "logs",
  "statement": "set(attributes[\"level\"], body[\"level\"])",
  "condition matched": true,
  "TransformContext": {
    "resource": { "attributes": {}, "dropped_attribute_count": 0 },
    "scope": {
      "attributes": {},
      "dropped_attribute_count": 0,
      "name": "",
      "version": ""
    },
    "log_record": {
      "attributes": { "level": "info" },
      "body": "{\"grpc.code\":\"OK\",\"grpc.method\":\"Check\",\"grpc.service\":\"grpc.health.v1.Health\",\"grpc.start_time\":\"2024-07-25T20:13:35Z\",\"grpc.time_ms\":\"0.025\",\"kubernetes\":{\"annotations\":{\"checksum/cm\":\"791ce46261793132cce6264086957ff301eb510e680ed9355a205a22056e9a5f\",\"checksum/cmd-params\":\"1c4495969eb3ee4e704035c6767fa421040dedd9ba5e3c28b8b610b34a56506f\"},\"container_hash\":\"quay.io/argoproj/argocd@sha256:d2c274ff26c7ab164907de05826bdfe2e6f326af70edd0bb83194b75fbb71f9e\",\"container_image\":\"quay.io/argoproj/argocd:v2.11.2\",\"container_name\":\"repo-server\",\"docker_id\":\"aeb425ec61ac163105b6271b8dc15718333d51c31ec797a5a3a61221b346e467\",\"host\":\"nuc-1\",\"labels\":{\"app.kubernetes.io/component\":\"repo-server\",\"app.kubernetes.io/instance\":\"argo-cd\",\"app.kubernetes.io/managed-by\":\"Helm\",\"app.kubernetes.io/name\":\"argocd-repo-server\",\"app.kubernetes.io/part-of\":\"argocd\",\"app.kubernetes.io/version\":\"v2.11.2\",\"helm.sh/chart\":\"argo-cd-6.11.1\",\"pod-template-hash\":\"54d8b9cf4d\"},\"namespace_name\":\"argocd\",\"pod_id\":\"d22d24f6-ff93-4740-84d0-9e8b657e5454\",\"pod_name\":\"argo-cd-argocd-repo-server-54d8b9cf4d-gfnz7\"},\"level\":\"info\",\"msg\":\"finished unary call with code OK\",\"severityText\":\"INFO\",\"span.kind\":\"server\",\"system\":\"grpc\",\"time\":\"2024-07-25T20:13:35Z\"}",
      "dropped_attribute_count": 0,
      "flags": 0,
      "observed_time_unix_nano": 0,
      "severity_number": 0,
      "severity_text": "INFO",
      "span_id": "0000000000000000",
      "time_unix_nano": 1721938415784407615,
      "trace_id": "00000000000000000000000000000000"
    },
    "cache": {}
  },
  "trace_id": "c055f3773f0383aaf9bd347fa88dab9c",
  "span_id": "16665a8cb4936e16"
}
```



