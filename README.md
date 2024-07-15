Step [1]: Install aws cli,eksctl,kubectl & aws configure

https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
https://eksctl.io/installation/
https://kubernetes.io/docs/tasks/tools/

- aws configure
- aws sts get-caller-identity

###

Step [2]: Create ClusterConfig yaml file & Create the Cluster

Copy from: https://raw.githubusercontent.com/aws-samples/eks-workshop-v2/stable/cluster/eksctl/cluster.yaml

- eksctl create cluster -f cluster.yaml

###

Step [3]: Connect kubectl to an EKS cluster by creating a kubeconfig file

- aws eks update-kubeconfig --region <region> --name <cluster-name>


