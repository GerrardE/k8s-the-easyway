## Initialize The Cluster

- Initialize the cluster on the control plane using kubeadm

`sudo kubeadm init --pod-network-cidr 192.168.0.0/16 --kubernetes-version 1.24.0`

- Setup the kubeconfig file:

`mkdir -p $HOME/.kube`

`sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config`

`sudo chown $(id -u):$(id -g) $HOME/.kube/config`

- Install Calico Newtork Addon:

`kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml`

- Check status of the control plane nodes:

`kubectl get nodes`
