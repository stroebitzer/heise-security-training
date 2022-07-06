
# Upgrade User Clusters


Check on an existing cluster the upgrade possibilities

![](../pics/upgrade_user_clusters.png)

<!-- TODO Slides kubernetes components version diffs -->

## Manage the available Kubernetes versions

Add the following to the file `kubermatic.yaml` in the `spec` section (mind the proper indent):

```yaml
versions:
  versions:
    - v1.20.13
    - v1.20.14
    - v1.21.8
    - v1.22.5
    - v1.22.10
    - v1.22.11
  default: '1.21.8'
```

Apply the updated Kubermatic configuration

```bash
kubectl apply -f ~/kkp/kubermatic.yaml
```

## Upgrae of User Cluster with UI

Within the UI upgrade your cluster to version `1.22.5`. Also check the checkbox `Upgrade Machine Deployments`

Watch the progress of the MachineDeployment upgrade (note you have to be connected to the User Cluster):

```bash
watch -n 1 kubectl get nodes
```

## Upgrade of User Cluster in Terminal

### Upgrade the Control Plane 

Change the field `spec.version` of the User Cluster to `1.22.11`.

```bash
kubectl edit cluster 
```

### Upgrade the Worker Nodes

Connected to the User Cluster you can change the version of the MachineDeployment via the following. Change the version of the field `spec.template.spec.versions.kubelet` to `1.22.11`.

```bash
kubectl -n kube-system edit md XXXXX

# Watch the nodes getting upgraded
watch -n1 kubectl get nodes   
```

<!-- TODO remove the deletion of cluster in prev step -->

<!-- TODO links to nect task -->

<!-- TODO tip kubermatic-installer print -->