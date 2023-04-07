---
title: "AWX"
date: 2023-01-17T14:56:04+01:00
draft: false
---

# How to install Awx using kubernetes operator
To install AWX using Kubernetes Operator, follow these steps:

1. Navigate to the awx-operator directory:

```bash
$ cd helm_charts/awx_chart/awx-operator
```

2. Verify the content of the following files:

- In kustomization.yaml, you can specify the version of AWX operator. 
```
 kustomization.yaml 
```
- In awx.yml, you can modify the specs of AWX to your needs.
```
 awx.yml 
```

3. Run the kustomize command to build the Kubernetes manifest and apply it:
```
$ kustomize build . | kubectl apply -f -
```