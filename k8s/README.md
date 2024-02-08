# K8s services

A little how to what this is and what it's used for. The whole point for this K8s lab setup is to learn and test the ways of Kubernetes. In order to do so, I've built a 3 server node Kubernetes cluster and strapped on some monitoring. I'm sure there are probably better ways of doing things, like Helm and etc., but bare in mind this is a local lab without Cloud as a backend, so not everything works out-of-the-box.

With all that in mind, here are the steps and services that are deployed, and the prefered order of things.

## 1. metrics-server

[README.md](./metrics-server/README.md)

Scalable and efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. [source](https://github.com/kubernetes-sigs/metrics-server)

Basically, allows you to run `kubectl top [node | pod]` and get basic CPU and RAM usage. In addition, this allows Kubernetes Dashboard to display the same information in it's web UI.
