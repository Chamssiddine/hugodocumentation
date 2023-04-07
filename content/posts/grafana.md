---
title: "Grafana"
date: 2023-01-14T14:56:27+01:00
draft: false
---

To deploy Grafana using the Helm Chart, follow these steps:

1. Navigate to the Grafana helm chart directory:

```
 $ cd helm_charts/grafana_chart

```

2. Add the Grafana Helm repository:

```
 $ helm repo add grafana
```

3. Install Grafana using the Helm Chart. We provided a customized `grafana_values.yaml` file for our specific needs, but you can modify it according to your preferences.

```
 helm install Grafana grafana/grafana -f grafana_values.yaml

```

4. After the installation is complete, you can access the Grafana dashboard using the IP address or hostname of the Kubernetes cluster along with the port number. I set it, to Grafana service IP.