---
{"dg-publish":true,"permalink":"/kubernetes/fluent-bit-konfiguracziya-logiv-dlya-flux-cd/","tags":["fluent-bit","monitoring","kubernetes","grafana","logs","observability"]}
---


`/etc/fluent-bit/fluent-bit.conf`:
```
[INPUT]
    Name tail
    Tag flux.*
    Path /var/log/containers/helm-controller-*,/var/log/containers/kustomize-controller-*,/var/log/containers/source-controller-*,/var/log/containers/notification-controller-*
    Parser flux_cri
    Mem_Buf_Limit 5MB
    Skip_Long_Lines On

[FILTER]
    Name kubernetes
    Match flux.*
    Regex_Parser kube-custom

[OUTPUT]
    name loki
    host localhost
    port 3100
    match flux.*
    labels app=flux, $level
    auto_kubernetes_labels on
```
    
`/etc/fluent-bit/parsers.conf`:
```
[PARSER]
    Name flux_cri
    Format regex
    Regex ^(?<time>[^ ]+) (?<stream>stdout|stderr) (?<logtag>[^ ]*) (?<message>.*)$
    Time_Key    time
    Time_Format %Y-%m-%dT%H:%M:%S.%L%z
    Time_Keep   On
    Decode_Field json message
```
![Selection_047.png](/img/user/Selection_047.png)