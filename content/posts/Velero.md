---
title: "Velero"
date: 2023-01-14T14:56:27+01:00
draft: false
---

1. Navigate to the Velero chart directory:

```
cd helm_charts/velero

```


2. Add the velero Helm chart repository from vmware github repo:

```
helm repo add vmware-tanzu https://vmware-tanzu.github.io/helm-charts

```
3. Install velero using the Helm chart. We provided the chart values customized for our needs, but you can make your changes as you wish. Specify the custom values file with -f flag:

```
helm install velero vmware-tanzu/velero --namespace velero -f values.yaml

```

This will deploy capsule in your Kubernetes cluster using the specified configuration in values.yaml file.

4. Show the status of the helm chart
```
helm status capsule -n capsule-system
```
