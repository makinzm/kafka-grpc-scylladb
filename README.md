# kafka-grpc-scylladb

## 1. How to create k8s cluster

- [Create a Multi-Node Cluster with k3d | Rancher Desktop Docs](https://docs.rancherdesktop.io/how-to-guides/create-multi-node-cluster/)
- [K3d cluster create - k3d](https://k3d.io/v5.0.0/usage/commands/k3d_cluster_create/)

```shell
k3d cluster create kafka-scylladb-cluster --api-port 6550 -p "8080:80@loadbalancer" --agents 3
```

```shell
k config get-contexts
```

## 2. How to k8s create namespace & Kafka cluster on k8s cluster

[Quickstarts](https://strimzi.io/quickstarts/)

```shell
kubectl create namespace kafka
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka

kubectl apply -f https://strimzi.io/examples/latest/kafka/kraft/kafka-single-node.yaml -n kafka
```

