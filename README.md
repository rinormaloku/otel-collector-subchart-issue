
Create a cluster
```
kind create cluster --image=kindest/node:v1.24.3
```

Generate template and apply to cluster
```
helm template . | kubectl apply -f - 
```

Output:

```
serviceaccount/release-name-metrics-gateway created
serviceaccount/release-name-demo-sub-charts created
configmap/release-name-metrics-gateway-agent created
service/release-name-demo-sub-charts created
deployment.apps/release-name-demo-sub-charts created
pod/release-name-demo-sub-charts-test-connection created
The DaemonSet "release-name-metrics-gateway-agent" is invalid: 
* spec.template.spec.volumes[0].name: Invalid value: "metricsGateway-configmap": a lowercase RFC 1123 label must consist of lower case alphanumeric characters or '-', and must start and end with an alphanumeric character (e.g. 'my-name',  or '123-abc', regex used for validation is '[a-z0-9]([-a-z0-9]*[a-z0-9])?')
* spec.template.spec.containers[0].name: Invalid value: "metricsGateway": a lowercase RFC 1123 label must consist of lower case alphanumeric characters or '-', and must start and end with an alphanumeric character (e.g. 'my-name',  or '123-abc', regex used for validation is '[a-z0-9]([-a-z0-9]*[a-z0-9])?')
* spec.template.spec.containers[0].volumeMounts[0].name: Not found: "metricsGateway-configmap"
```

Focus on the violations. The first one is about the name of the configmap. The second one is about the name of the container. The third one is about the name of the volumeMounts.