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


## Test
```
export MONGODB_ROOT_PASSWORD=$(kubectl get secret --namespace dev mymongo-mongodb -o jsonpath="{.data.mongodb-root-password}" | base64 --decode)
kubectl run --namespace dev mongodb-client --rm --tty -i --restart='Never' --image docker.io/bitnami/mongodb:4.4.1-debian-10-r13 --command -- bash
mongo admin --host "mymongo-mongodb-0.mymongo-mongodb-headless.dev.svc.cluster.local,mymongo-mongodb-1.mymongo-mongodb-headless.dev.svc.cluster.local," --authenticationDatabase admin -u root -p $MONGODB_ROOT_PASSWORD

show dbs
use sampledb
show collections
db.pizza.find().pretty()
```

