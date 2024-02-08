# K8s services

A little how to what this is and what it's used for. The whole point for this K8s lab setup is to learn and test the ways of Kubernetes. In order to do so, I've built a 3 server node Kubernetes cluster and strapped on some monitoring. I'm sure there are probably better ways of doing things, like Helm and etc., but bare in mind this is a local lab without Cloud as a backend, so not everything works out-of-the-box.

With all that in mind, here are the steps and services that are deployed, and the prefered order of things.

## 0. Debug / BusyBox

K8s SwissKnife / debug box. This command runs it in `monitoring` namespace, interactive shell and deletes itself after exit to leave it all clean.

```bash
kubectl -n monitoring run -i --rm --tty busybox --image=busybox --restart=Never -- sh
```

## 1. metrics-server

[README.md](./metrics-server/)

Scalable and efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines [source](https://github.com/kubernetes-sigs/metrics-server).

Basically, allows you to run `kubectl top [node | pod]` and get basic CPU and RAM usage. In addition, this allows Kubernetes Dashboard to display the same information in it's web UI.

## 2. kube-state-metrics

[README.md](./kube-state-metrics/)

Add-on agent to generate and expose cluster-level metrics [source](https://github.com/kubernetes/kube-state-metrics).

There a whole bunch of documentation about this, but in a nutshell - it exposes metrics to Prometheus.

## 3. dashboard

[README.md](./dashboard/)

General-purpose web UI for Kubernetes clusters [source](https://github.com/kubernetes/dashboard).

It says it all.

## 4.1. kube-prometheus-stack (Helm)

[README.md](./kube-prometheus-stack/)

Installs the kube-prometheus stack, a collection of Kubernetes manifests, Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end Kubernetes cluster monitoring with Prometheus using the Prometheus Operator [source](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack).

This thing installs a bunch of stuff, but not everything works on the local Lab without adjustments, thus there is the next option.

## 4.2. monitoring

[README.md](./monitoring/)

Adjusted version of `kube-prometheus-stack` for the local Lab environment (still a work in progress).

At the moment it contains:

* Separate namespace `monitoring`
* Prometheus and Grafana deployments
* Prometheus exporters:
  * Blackbox - for HTTP, TCP, etc.
  * SNMP - for SNMP walks
