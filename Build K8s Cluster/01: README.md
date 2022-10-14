## Build A Kubernetes Cluster With Kubeadm

- First, log onto the control plane node and the worker nodes:

`ssh cloud_user@<PUBLIC_IP_ADDRESS>`

- Setup the hostname of each node:

`sudo hostnamectl set-hostname k8s-control`

- Setup hostfile with mappings for the servers to communicate with each other:

`sudo vi /etc/hosts`

```
Cloud Server Hostname Mapping
<Private IP control-node1> <Hostname mapping of control node 1>
<Private IP control-node2> <Hostname mapping of control node 2>
<Private IP worker-node1> <Hostname mapping of worker node 1>
<Private IP worker-node2> <Hostname mapping of worker node 2>
```

Log out and log back in to each server to see the updates

