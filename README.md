# multi-stage-helm-chart-demo

helm upgrade -i multi-stage charts/multi-stage

```
{{if not (lookup "v1" "Namespace" "" "demo") }}{{ fail "Namespace demo is required" }}{{ end }}
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ include "multi-stage.serviceAccountName" . }}
  annotations:
  {{- range $k,$v := (lookup "v1" "Namespace" "" "kube-system").metadata.labels }}
    {{$k}}: {{$v}}
  {{- end }}
data:
  a: b
```