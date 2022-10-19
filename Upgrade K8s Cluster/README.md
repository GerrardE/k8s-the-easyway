## Upgrade A Kubernetes Cluster With Kubeadm

- Log into the control plane server:

`ssh cloud_user@<PUBLIC_IP_ADDRESS>`

##### Upgrade The Control Plane
- Update all control plane components(make sure to override the held* upgrades)

`sudo apt-get update && sudo apt-get install -y --allow-change-held-packages kubeadm=1.22.2-00`

confirm upgrade version `kubeadm version`

- Drain the control plane node(draining a node actually cordons it):

`kubectl drain k8s-control --ignore-daemonsets`

- Plan the upgrade:

`sudo kubeadm upgrade plan v1.22.2`

- Run the resulting planned upgrade command as root:

`sudo kubeadm upgrade apply v1.22.2`

- Upgrade kubelet and the kubectl on the control plane:

`sudo apt-get update && sudo apt-get install -y --allow-change-held-packages kubelet=1.22.2-00 kubectl=1.22.2-00`

- Restart the kubelet:

`sudo systemctl daemon-reload`

`sudo systemctl restart kubelet`

- Uncordon the control plane node:

`kubectl uncordon k8s-control`

- Verify `kubectl get nodes`

##### Upgrade The Worker Nodes

- From the control plane, drain the worker node:

`kubectl drain k8s-worker1 --ignore-daemonsets --force`

- Upgrade kubeadm:

`sudo apt-get update && sudo apt-get install -y --allow-change-held-packages kubeadm=1.22.2-00`

- Upgrade kubelet config:

`sudo kubeadm upgrade node`

- Upgrade kubelet and kubectl:

`sudo apt-get update && sudo apt-get install -y --allow-change-held-packages kubelet=1.22.2-00 kubectl=1.22.2-00`

- Restart the kubelet:

`sudo systemctl daemon-reload`

`sudo systemctl restart kubelet`

- Uncordon the node from the control plane:

`kubectl uncordon <worker-node>`
