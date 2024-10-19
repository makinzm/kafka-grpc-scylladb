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

## 2. How to create k8s namespace & Kafka cluster on k8s cluster

[Quickstarts](https://strimzi.io/quickstarts/)

```shell
kubectl create namespace kafka
kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka

kubectl apply -f https://strimzi.io/examples/latest/kafka/kraft/kafka-single-node.yaml -n kafka
```

## 3. How to create ScyllaDB Operator on k8s

[Deploying Scylla on a Kubernetes Cluster | ScyllaDB Docs](https://operator.docs.scylladb.com/stable/generic.html)

```shell
cd scylla-operator


kubectl apply -f examples/common/cert-manager.yaml

kubectl wait --for condition=established crd/certificates.cert-manager.io crd/issuers.cert-manager.io
kubectl -n cert-manager rollout status deployment.apps/cert-manager-webhook

kubectl apply -f deploy/operator.yaml

kubectl wait --for condition=established crd/scyllaclusters.scylla.scylladb.com
kubectl -n scylla-operator rollout status deployment.apps/scylla-operator

kubectl -n scylla-operator logs deployment.apps/scylla-operator
```

```shell
k get deployments --all-namespaces
```

```
NAMESPACE         NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
cert-manager      cert-manager                 1/1     1            1           7m48s
cert-manager      cert-manager-cainjector      1/1     1            1           7m48s
cert-manager      cert-manager-webhook         1/1     1            1           7m48s
kafka             my-cluster-entity-operator   1/1     1            1           17m
kafka             strimzi-cluster-operator     1/1     1            1           34m
kube-system       coredns                      1/1     1            1           43m
kube-system       local-path-provisioner       1/1     1            1           43m
kube-system       metrics-server               1/1     1            1           43m
kube-system       traefik                      1/1     1            1           40m
scylla-operator   scylla-operator              2/2     2            2           5m24s
scylla-operator   webhook-server               2/2     2            2           5m24s
```

## 4. How to create Scylla db cluster

```shell
kubectl create -f examples/generic/cluster.yaml

kubectl -n scylla get ScyllaCluster

```

```
❯ k get ns
NAME              STATUS   AGE
cert-manager      Active   13m
default           Active   48m
kafka             Active   40m
kube-node-lease   Active   48m
kube-public       Active   48m
kube-system       Active   48m
scylla            Active   2m2s
scylla-operator   Active   10m
```

```shell
❯ kubectl -n scylla get pods
No resources found in scylla namespace.

```

### 4.1. The reason no pod exists


