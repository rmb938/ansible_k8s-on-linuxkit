# ansible_k8s-on-linuxkit
Ansible to automate https://github.com/rmb938/k8s-on-linuxkit

## Host Groups

### `init-master`

Typically your first kubernetes master in the cluster. This will be the node the cluster is initialized on

### `masters`

Additional masters you want to join the cluster

### `workers`

Additional workers you want to join the cluster

## Group Variables

### `clusterName`

The cluster name, this is only visable in kubeconfigs generated by kubeadm

### `podSubnet`

The subnet pod IPs come from

### `serviceSubnet`

The subnet service IPs come from

### `controlPlaneEndpoint`

This is the control plane endpoint. This should point to a LoadBalancer with all the control plane nodes listening on port 6443. When setting this variable do not include a port.

If you don't have a load balancer this can simply be the `init-master` node however you shouldn't do this in production.

## Usage

This playbook uses [kube-router](https://github.com/cloudnativelabs/kube-router) as the CNI.

1. Create a cluster inside of the `clusters` folder.
  * Use the `local` cluster as an example
1. Run `ansible-playbook -i clusters/${your_cluster}/hosts site.yaml --verbose`

If you want to customize the kubeadm configuration or change the CNI fork this repo and modify it as needed.

## TODO

- [X] Allow a DNS record to be given for the control plane
  * When it is given add it to the correct certificates
- [ ] Figure out a way to get `caCertHashes` so nodes can join securely
- [ ] Allow nodes to join with taints and labels
