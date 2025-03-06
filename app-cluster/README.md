## Pre-requisites

* Install `kube-state-metrics` :

`helm install kube-state-metrics prometheus-community/kube-state-metrics`

* Install node-exporter:

`helm install nodeexporter prometheus-community/prometheus-node-exporter -n default`

* Install otel collector helm chart

`helm upgrade --install otel open-telemetry/opentelemetry-collector -f otel.yaml`


* Install otel demo

`helm upgrade --install otel-demo open-telemetry/opentelemetry-demo -f otel-demo.yaml`


** Note:

Ensure your otel demo values file sets something like this:
```
default:
  envOverrides:
      - name: OTEL_COLLECTOR_NAME
        value: otel-opentelemetry-collector
      - name: OTEL_RESOURCE_ATTRIBUTES
        value: 'service.name=$(OTEL_SERVICE_NAME),service.namespace=default,service.version={{ .Chart.AppVersion }}'

```

namely, the `service.namespace` bit. The default is `opentelemetry-demo`, which will result in broken links all over the place if your app is not deployed in the opentelemetry-demo namespace. 


