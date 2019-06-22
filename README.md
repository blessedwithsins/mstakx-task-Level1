# mstakx-tasks
1. Once kubeadm-install-master script has run successfully on master node, apply Network Plugin & run rest of the commands as normal user

Need to run as sudo:-

kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/bc79dd1505b0c8681ece4de4c0d86c5cd2643275/Documentation/kube-flannel.yml

Need to run as normal user:-

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

2. Once kubeadm-install-node script has run successfully on all worker nodes, run below command on each node to add it into the cluster.

Need to run as sudo:-

kubeadm join 10.128.0.2:6443 --token vxmceg.z8d6v1fdeiewngvx --discovery-token-ca-cert-hash sha256:4818f2b209cc1619c2690f654d0635b278cce19477c89c3ea962e1b72d403424

If you're unable to find the token, please run below command to generate a new one. 

kubeadm token create --print-join-command

3. To create namespaces, we can use imperative way. Both are described below:-

kubectl create ns staging
kubectl create ns production


