# Prometheus

## Namespace

```bash
kubectl apply -f k8s/prometheus/namespace.yml
```

## ConfigMap

```bash
# Render preview
kubectl kustomize k8s/prometheus/prometheus-conf

# Apply
kubectl apply -k k8s/prometheus/prometheus-conf
```

## RBAC

```bash
kubectl apply -f k8s/prometheus/clusterrole.yml
kubectl apply -f k8s/prometheus/clusterrolebinding.yml
```

## Deployment

```bash
kubectl apply -f k8s/prometheus/deployment.yml
```

## Service

```bash
kubectl apply -f k8s/prometheus/service.yml
```

## Access

Once all recources are deployed, you can access Prometheus on any of the cluster nodes' IP addresses. Pick one from the list:

```bash
kubectl get nodes -o wide
```

Then open in your browser: http://<NODE_IP>:30090/
