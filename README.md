# Minimum Viable Kube-ArangoDB

This repo demonstrates basic usage of [Kube-ArangoDB](https://github.com/arangodb/kube-arangodb), and uses [Kustomize](https://kustomize.io/) to do it.

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

With that running, you can connect to the admin interface by forwarding the ports to your local machine. The name of the pod will be different for you.
```
kubectl port-forward -n db arangodb-sngl-hamld3tu-7c02a6 8529:8529
Forwarding from 127.0.0.1:8529 -> 8529
Forwarding from [::1]:8529 -> 8529
```

With that you should be able to connect to [localhost:8529](http://localhost:8529/_db/_system/_admin/aardvark/index.html#login)
