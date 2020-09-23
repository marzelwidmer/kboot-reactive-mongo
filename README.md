# Install MongoDB with Helm on OpenShift

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

```
helm install mymongo -f values-openshift.yaml bitnami/mongodb
```


# Deploy
```
skaffold run
```
