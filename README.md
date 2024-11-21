## Description

This repository contains helm chart for the following apps & services deployment within Kubernetes cluster:

* [Spam2000 app](https://hub.docker.com/r/andriiuni/spam2000) - custom application with monitoring metrics
* VictoriaMetrics Cluster - Kubernetes cluster monitoring
* VictoriaMetrics Agent - monitoring metrics scraping
* Grafana - visual dashboards for K8s cluster and Spam2000 app


## Prerequisites

Install the following packages & versions: 

* Kubectl v.1.22.* or higher: https://kubernetes.io/releases/download/#kubectl
* helm 3.14.0 or higher: https://github.com/helm/helm/releases


## How to install

1.  Clone current repository locally

2. From the root of the repo run the following command:
```console
helm install k8s-monitoring ./charts/
```

## Credits

https://docs.victoriametrics.com/guides/k8s-monitoring-via-vm-cluster/
https://docs.victoriametrics.com/helm/victoriametrics-cluster/index.html
https://github.com/VictoriaMetrics/helm-charts/tree/master/charts/victoria-metrics-cluster
https://github.com/VictoriaMetrics/helm-charts/tree/master/charts/victoria-metrics-agent