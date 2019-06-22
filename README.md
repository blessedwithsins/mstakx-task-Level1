# mstakx-task-Level1

1. Run kubeadm-install-master.sh to install Kubeadm, Kubectl & Docker on master node along with Network Plugin after cluster initialization.

2. Once kubeadm-install-node script has run successfully on all worker nodes, run below command on each node to add it into the cluster.

Need to run as sudo:-

kubeadm join 10.128.0.2:6443 --token vxmceg.z8d6v1fdeiewngvx --discovery-token-ca-cert-hash sha256:4818f2b209cc1619c2690f654d0635b278cce19477c89c3ea962e1b72d403424

If you're unable to find the token, please run below command to generate a new one. 

kubeadm token create --print-join-command

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



