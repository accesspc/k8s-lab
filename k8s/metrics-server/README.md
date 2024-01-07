# Kubernetes Metrics Server

This is a copy of components.yaml release v0.6.4 [GitHub](https://github.com/kubernetes-sigs/metrics-server/releases), with a minor change in Deployment -> Template -> Container['metrics-server'] -> args: `--kubelet-insecure-tls=true`

## Installation

```bash
kubectl apply -f k8s/metrics-server/components.yaml
```
