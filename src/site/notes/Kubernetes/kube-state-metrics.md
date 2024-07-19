---
{"dg-publish":true,"permalink":"/kubernetes/kube-state-metrics/","tags":["tools","kubernetes","metrics","monitoring","observability","prometheus","prometheus-exporter"]}
---

Встановлюється в Kubernetes.

Метрики можна збирати за допомогою prometheus.

kube-state-metrics (KSM) is a simple service that listens to the Kubernetes API server and generates metrics about the state of the objects. (See examples in the Metrics section below.) It is not focused on the health of the individual Kubernetes components, but rather on the health of the various objects inside, such as deployments, nodes and pods.