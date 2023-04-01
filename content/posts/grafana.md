---
title: "Grafana"
date: 2023-01-14T14:56:27+01:00
draft: false
---

Once you're inside the git repo travel to helm chart for Grafana

<br>

  `$ cd helm_charts/grafana_chart` 
<br>
## install helm repo from codecentric 

    - helm repo add grafana

## install Grafana using helm chart

We provided the chart values customized for our needs but you can make your changes as you wish.

To proced the deployment of Grafana type in

    - helm install Grafana grafana/grafana -f grafana_values.yaml