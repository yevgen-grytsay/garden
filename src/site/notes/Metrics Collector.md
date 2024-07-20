---
{"dg-publish":true,"permalink":"/metrics-collector/","tags":["metrics","monitoring","prometheus-exporter","prometheus","observability"]}
---

## OS Metrics
- https://hub.docker.com/r/prom/node-exporter
- [[Kubernetes/Fluent-Bit\|Fluent-Bit]] with input plugin node_exporter_metrics. Правда є імовірність, що через цей плагін Fluent-bit час від часу крешиться (v3.0.7).
## Container Metrics
- [[cAdvisor\|cAdvisor]] https://github.com/google/cadvisor/blob/master/docs/storage/prometheus.md
- [[Kubernetes/kube-state-metrics\|kube-state-metrics]]