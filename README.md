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
* For test purposes:
```console
helm install monitoring-k8s ./charts/ --dry-run
```
* For deployment:
```console
helm install monitoring-k8s ./charts/ 
```

The desired output should be similar to the following:
```console
NAME: monitoring-k8s
LAST DEPLOYED: Thu Nov 28 16:02:10 2024
NAMESPACE: default
STATUS: deployed
REVISION: 1
```

All resources will be created within the default namespace.
In order to check resources status run command below:
```console
kubectl get all
```

The expected result should look like the following:
```console
NAME                                                                  READY   STATUS    RESTARTS   AGE
pod/monitoring-k8s-grafana-7747df6f65-jhjtn                           2/2     Running   0          6m33s
pod/monitoring-k8s-victoria-metrics-agent-b96ddc8b9-2k6vp             1/1     Running   0          6m33s
pod/monitoring-k8s-victoria-metrics-cluster-vminsert-7859d4949rjjqs   1/1     Running   0          6m33s
pod/monitoring-k8s-victoria-metrics-cluster-vmselect-757476d44cw69h   1/1     Running   0          6m33s
pod/monitoring-k8s-victoria-metrics-cluster-vmstorage-0               1/1     Running   0          6m33s
pod/spam-app-b9989dc6-89hdg                                           1/1     Running   0          6m33s

NAME                                                        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                      AGE
service/kubernetes                                          ClusterIP   10.96.0.1        <none>        443/TCP                      25h
service/monitoring-k8s-grafana                              ClusterIP   10.108.126.118   <none>        80/TCP                       6m33s
service/monitoring-k8s-victoria-metrics-cluster-vminsert    ClusterIP   10.111.73.81     <none>        8480/TCP                     6m33s
service/monitoring-k8s-victoria-metrics-cluster-vmselect    ClusterIP   10.111.252.215   <none>        8481/TCP                     6m33s
service/monitoring-k8s-victoria-metrics-cluster-vmstorage   ClusterIP   None             <none>        8482/TCP,8401/TCP,8400/TCP   6m33s
service/spam-app                                            ClusterIP   10.103.64.211    <none>        3000/TCP                     6m33s

NAME                                                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/monitoring-k8s-grafana                             1/1     1            1           6m33s
deployment.apps/monitoring-k8s-victoria-metrics-agent              1/1     1            1           6m33s
deployment.apps/monitoring-k8s-victoria-metrics-cluster-vminsert   1/1     1            1           6m33s
deployment.apps/monitoring-k8s-victoria-metrics-cluster-vmselect   1/1     1            1           6m33s
deployment.apps/spam-app                                           1/1     1            1           6m33s

NAME                                                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/monitoring-k8s-grafana-7747df6f65                             1         1         1       6m33s
replicaset.apps/monitoring-k8s-victoria-metrics-agent-b96ddc8b9               1         1         1       6m33s
replicaset.apps/monitoring-k8s-victoria-metrics-cluster-vminsert-7859d49495   1         1         1       6m33s
replicaset.apps/monitoring-k8s-victoria-metrics-cluster-vmselect-757476d44b   1         1         1       6m33s
replicaset.apps/spam-app-b9989dc6                                             1         1         1       6m33s

NAME                                                                 READY   AGE
statefulset.apps/monitoring-k8s-victoria-metrics-cluster-vmstorage   1/1     6m33s
```

If some item is not in Running status - inspect it with the following commands:
```console
kubectl describe <item_name>
kubectl logs -f <pod_name>
```

## Credits

https://docs.victoriametrics.com/guides/k8s-monitoring-via-vm-cluster/
https://docs.victoriametrics.com/helm/victoriametrics-cluster/
https://github.com/VictoriaMetrics/helm-charts/tree/master/charts/victoria-metrics-cluster/
https://github.com/VictoriaMetrics/helm-charts/tree/master/charts/victoria-metrics-agent/