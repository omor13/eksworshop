Step [1]: Install aws cli,eksctl,kubectl & aws configure

1. https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
2. https://eksctl.io/installation/
3. https://kubernetes.io/docs/tasks/tools/

- aws configure
- aws sts get-caller-identity

###

Step [2]: Create the Cluster using yaml file

- eksctl create cluster -f cluster.yaml

###

Step [3]: Connect kubectl to an EKS cluster by creating a kubeconfig file

- aws eks update-kubeconfig --region <region> --name <cluster-name>

###

Step [4]: deploy all components using kubectl apply

- kubectl apply - f deploy.yaml


