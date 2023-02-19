# Local Kuberntes (Docker Desktop)


## Kuberntes Dashboard

[Deploy and Access the Kubernetes Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/):

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
kubectl proxy
```

Edit deployment YAML manifest to skip dashboard authentication:

```
kuberntes edit kubernetes-dashboard -n kubernetes-dashboard
```

```yaml
spec:
  template:
    spec:
      containers:
      - args:
        - --auto-generate-certificates
        - --namespace=kubernetes-dashboard
        - --enable-skip-login  # add skip login args
```

Connect the dashboard via following URL:

http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/cronjob?namespace=default

[Resolve permission errors with dashboard](https://github.com/kubernetes/dashboard/issues/4179):

```
kubectl apply -f kubernetes-dashboard.yaml
```

