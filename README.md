Step [1]: Install aws cli,eksctl,kubectl,helm & aws configure

1. https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
2. https://eksctl.io/installation/
3. https://kubernetes.io/docs/tasks/tools/
4. https://helm.sh/docs/intro/install/

- aws configure
- aws sts get-caller-identity

###

Step [2]: Create the Cluster using yaml file

- eksctl create cluster -f cluster-with-addons.yaml

###

Step [3]: Connect kubectl to an EKS cluster by creating a kubeconfig file

- aws eks update-kubeconfig --region <region> --name <cluster-name>

###

Step [4] Install AWS Load Balancer Controller

curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.7.2/docs/install/iam_policy.json
aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam_policy.json
eksctl create iamserviceaccount \
  --cluster=<my-cluster> \
  --namespace=kube-system \
  --name=aws-load-balancer-controller \
  --role-name AmazonEKSLoadBalancerControllerRole \
  --attach-policy-arn=arn:aws:iam::590692511501:policy/AWSLoadBalancerControllerIAMPolicy \
  --approve

helm repo add eks https://aws.github.io/eks-charts
helm repo update eks
helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=<my-cluster> \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller 

###

Step [5]: deploy all components using kubectl apply

- kubectl apply -f deploy.yaml

Step [6] Delete Resources

- eksctl delete cluster <cluster-name>