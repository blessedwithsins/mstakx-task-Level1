# mstakx-tasks
1. Once kubeadm-install script has run successfully on master node, apply Network Plugin & run rest of the commands as normal user

Need to run as sudo:-

kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/bc79dd1505b0c8681ece4de4c0d86c5cd2643275/Documentation/kube-flannel.yml

Need to run as normal user:-

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

