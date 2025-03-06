## Pre-requisites

* Store Grafana Cloud credentials as a secret:

`kubectl create secret generic otel-secret --from-literal=otel-pass=YOUR_ACCESS_TOKEN --from-literal=otel-userid=YOUR_USERID`

_These are referenceable through typical environment variable string interpolation in yaml_:

```yaml
config:
  extensions:
    health_check: {}
    basicauth/grafana_cloud:
      client_auth:
        username: ${OTELUSERID}
        password: ${OTELPASS}
```



* Install `kube-state-metrics` :

`helm install kube-state-metrics prometheus-community/kube-state-metrics`

* Install node-exporter:

`helm install nodeexporter prometheus-community/prometheus-node-exporter -n default`

* Install otel collector helm chart

`helm upgrade --install otel open-telemetry/opentelemetry-collector -f otel.yaml`

