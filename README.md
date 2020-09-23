# Install MongoDB with Helm on OpenShift

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

```
helm install mymongo -f values-openshift.yaml bitnami/mongodb
```
## Test
```
export MONGODB_ROOT_PASSWORD=$(kubectl get secret --namespace dev mongodb -o jsonpath="{.data.mongodb-root-password}" | base64 --decode)
kubectl run --namespace dev mongodb-client --rm --tty -i --restart='Never' --image docker.io/bitnami/mongodb:4.4.1-debian-10-r13 --command -- bash
mongo admin --host "mongodb-0.mongodb-headless.dev.svc.cluster.local,mongodb-1.mongodb-headless.dev.svc.cluster.local," --authenticationDatabase admin -u root -p $MONGODB_ROOT_PASSWORD
```


# Deploy Application
```
skaffold run
```



