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

3. To create namespaces, we can use imperative way via below command:- 
kubectl create ns staging

kubectl create ns production

4. Installing guest-book application on both namespaces as below:-

git clone https://github.com/kubernetes/examples.git

After cloning of repository, apply only the necessary files via below command:-

kubectl -n staging apply -f examples/

kubectl -n production apply -f examples/

5/6. Create Ingress yaml to expose application service via hostname. Files are uploaded in repository master branch. 

7. Horizontal pod autoscaler can be created via below command:-

kubectl -n production autoscale deployment frontend --cpu-percent=90 --min=1 --max=3

kubectl -n staging autoscale deployment frontend --cpu-percent=90 --min=1 --max=3

8. For monitoring of pod autoscaling during Load & performance testing, I'm using metrics-server.

git clone https://github.com/linuxacademy/metrics-server

kubectl apply -f ~/metrics-server/deploy/1.8+/

kubectl get --raw /apis/metrics.k8s.io/

kubectl top po --all-namespaces 

List of documentation followed for this task:-

https://kubernetes.io/docs/tutorials/stateless-application/guestbook/
https://cloud.google.com/community/tutorials/nginx-ingress-gke
https://github.com/helm/helm/blob/master/docs/install.md
https://itnext.io/save-costs-in-your-kubernetes-cluster-with-5-open-source-projects-7f53899a1429
https://github.com/linuxacademy/metrics-server

Q. What was the node size chosen for the Kubernetes nodes? And why?

A. I've choosen a normal node with 1vCPU & 3.75GB memory as we're not running actual production grade load on the server. Also, this needs to be decided after Load & Performance testing for application depending on the requests being server by application. 

Q. What method was chosen to install the demo application and ingress controller on the cluster, justify the method used.

A. I used kubectl utility to deply demo application. To deploy ingress controller on the cluster, I used helm. Helm is one of the best tools to deploy application or cluster components as it takes care of dependencies plus you can create your own charts specific to your applications.

Q. What would be your chosen solution to monitor the application on the cluster and why?

A. I have used metrics-server here but we can use tools like Datadog, Instana, Prometheus, Grafana to monitor the application as well as cluster components. 

Q. What additional components / plugins would you install on the cluster to manage it better? 

A. 



