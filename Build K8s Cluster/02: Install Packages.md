## Install Packages

- Create a containerd config file:

```
cat <<EOF | sudo tee /etc/modules-load.d/containerd.conf
overlay
br_netfilter
EOF
```

- Load the modules

`sudo modprobe overlay`

`sudo modprobe br_netfilter`

- Setup system config for k8s networking

```
cat <<EOF | sudo tee /etc/sysctl.d/99-kubernetes-cri.conf
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
EOF
```

- Apply the new configurations

`sudo sysctl --system`

- Install the container runtime, containerd:

`sudo apt-get update && sudo apt-get install -y containerd`

- Setup default configuration for containerd:

`sudo mkdir -p /etc/containerd`

- Generate a default containerd config and save it to the newly created default file:

`sudo containerd config default | sudo tee /etc/containerd/config.toml`

- Restart contained for configurations to take effect:

`sudo systemctl restart containerd`

- Verify that containerd is running:

`sudo systemctl status containerd`

- Disable swap: `sudo swapoff -a`

- Install dependencies:

`sudo apt-get update && sudo apt-get install -y apt-transport-https curl`

- Download/add gpg key:

`curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -`

- Add k8s to repo list:

```
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

- Update package list: `sudo apt-get update`

- Install k8s packages:

`sudo apt-get install -y kubelet=1.24.0-00 kubeadm=1.24.0-00 kubectl=1.24.0-00`

- Turn off auto updates:

`sudo apt-mark hold kubelet kubeadm kubectl`

*N.B Rerun the above commands to get the worker nodes ready*
