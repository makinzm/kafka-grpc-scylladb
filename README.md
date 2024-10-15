# kafka-grpc-scylladb

## 1. How to create k8s cluster

- [minikube start | minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download)

```shell
# check my host os architecture
uname -m

# download minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64

# start cluster
minikube start --profile=kafka-grpc-scylladb-cluster
```

