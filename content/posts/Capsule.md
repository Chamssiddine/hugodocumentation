---
title: "Capsule"
date: 2023-01-14T14:56:27+01:00
draft: false
---

1. Navigate to the capsule chart directory:

```
cd helm_charts/capsule

```


2. Add the clastix Helm chart repository from calstix github repo:

```
helm repo add clastix https://clastix.github.io/charts
```
3. Install capsule using the Helm chart. We provided the chart values customized for our needs, but you can make your changes as you wish. Specify the custom values file with -f flag:

```
helm install capsule clastix/capsule -n capsule-system --create-namespace -f values.yaml

```

This will deploy capsule in your Kubernetes cluster using the specified configuration in values.yaml file.

4. Show the status of the helm chart
```
helm status capsule -n capsule-system
```
