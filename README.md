# Minimum Viable Kube-ArangoDB

This repo demonstrates basic usage of [Kube-ArangoDB](https://github.com/arangodb/kube-arangodb), and uses [Kustomize](https://kustomize.io/) and [Minikube](https://minikube.sigs.k8s.io/docs/) to do it.

## Getting started

Kustomize expects a `.env` file in the directory. You can create it with the following command. The values in that file will be used as the credentials for the root user.

```
cat <<'EOF' > arangodb.env
username=root
password=test
EOF
```

## Using it

```
minikube start
kustomize build . | kubectl apply -f -
```

You can watch the creation of the pods and pvc, and when it looks like this, you'll know it's ready.

```
$ kubectl get po,pvc -n db
NAME                                                          READY   STATUS    RESTARTS   AGE
pod/arango-deployment-operator-7c54bb947-67qdn                1/1     Running   0          3m49s
pod/arango-deployment-replication-operator-558b49f785-k99hf   1/1     Running   0          3m49s
pod/arango-storage-operator-68fb5f6949-zzf4c                  1/1     Running   0          3m49s
pod/arangodb-sngl-miotcqdv-435cf0                             2/2     Running   0          3m9s

NAME                                             STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/arangodb-single-miotcqdv   Bound    pvc-71fee7f0-2387-4985-a551-a79ab8671a34   10Gi       RWO            standard       3m9s
```

With that running, you can connect to the admin interface by forwarding the ports to your local machine.

```
kubectl port-forward -n db svc/arangodb 8529:8529
Forwarding from 127.0.0.1:8529 -> 8529
Forwarding from [::1]:8529 -> 8529
```

With that you should be able to connect to [localhost:8529](http://localhost:8529/_db/_system/_admin/aardvark/index.html#login), with the credentials you gave above.
