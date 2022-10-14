## Join Worker Nodes To The Cluster

- Create a join token from the control node 

`kubeadm token create --print-join-command`

- ssh to the worker nodes and run the command from step 1 as sudo, e.g:

`sudo kubeadm join 10.0.1.101:6443 --token 5w919m.zaog5u9te6so11xi --discovery-token-ca-cert-hash sha256:4699d0752cbeb3467a992277ef597cd34fdf7acc7e753fe137da657567df448f`

- From the control plane run `kubectl get nodes` to know the status of the nodes
