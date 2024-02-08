# Prometheus

## Access

Once all recources are deployed, you can access Prometheus and Grafana on any of the cluster nodes' IP addresses. Pick one from the list:

```bash
kubectl get nodes -o wide
```

## Namespace

```bash
kubectl apply -f k8s/monitoring/namespace.yml
```

## Blackbox

```bash
# ConfigMap: preview
kubectl kustomize k8s/monitoring/blackbox/config/

# Apply
kubectl apply -k k8s/monitoring/blackbox/config/
kubectl apply -f k8s/monitoring/blackbox/
```

## Prometheus

```bash
# ConfigMap: preview
kubectl kustomize k8s/monitoring/prometheus/config

# Apply
kubectl apply -k k8s/monitoring/prometheus/config
kubectl apply -f k8s/monitoring/prometheus
```

* Prometheus: http://<NODE_IP>:30090/

## Grafana

```bash
# Apply
kubectl apply -f k8s/monitoring/grafana
```

* Grafana: http://<NODE_IP>:30030/
