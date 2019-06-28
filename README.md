# Rook CEPH Helm Chart

This helm chart deploys a storage class with all underlying needs.
A rook installation with CEPH support is required to use this.

We assume that you want to be able to deploy multiple storage classes, so we decided to seperate namespaces. The rook operator can be deployed with it's [helm](https://rook.io/docs/rook/master/helm-operator.html) chart to a namespace of your choice. Storage classes should be deployed to seperate namespaces as only one CephPool can be created per namespace.

> After installation of the rook helm chart, you need to manually edit the deployment. You have to set `ROOK_CURRENT_NAMESPACE_ONLY` to `false`.

## Usage

values.yaml:
```yaml
storage:
  monCount: 1 # Monitor Count, should be 3, if possible.
  replicaCount: 1 # Filesystem Replica Count
  fileSystem: "xfs" # Filesystem
  failureDomain: "osd" # Replication Mode 

  nodes: # https://github.com/rook/rook/blob/master/Documentation/ceph-cluster-crd.md#node-settings
  - name: "node3"
    directories:
    - path: "/data/data1"

operator:
  namespace: "rook-ceph-system" # Namespace, where the operator is deployed to.

```
