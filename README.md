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
  ca.crt: |
    {{- dig "data" "ca.crt" "unknown" (lookup "v1" "ConfigMap" (printf "%s" .Release.Namespace) "kube-root-ca.crt") | nindent 4 }}
```