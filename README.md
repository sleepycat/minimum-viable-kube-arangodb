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
