# Kubernetes dashboard

[Official documentation](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)

## Installation

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
```

## Service Account for access

[Official documentation](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)

Create ServiceAccount and ClusterRoleBinding objects, then create a token for the new ServiceAccount admin-user in kubernetes-dashboard namespace:

```bash
kubectl apply -f k8s/dashboard/
kubectl -n kubernetes-dashboard create token admin-user
```

## Proxy

Run the following to proxy dashboard on to your machine:

```bash
kubectl proxy
```

Then open [http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/) and enter the token from the step below to access the dashboard.
