
## bootstrap cluster
```
ssh-keygen -t rsa -b 2048 -f ~/.ssh/id_xke_k8s_service

eval $(assume-role xebia-ocloirec)

eksctl create cluster \
--name xke-k8s-service \
--version 1.14 \
--nodegroup-name xke-k8s-service-workers \
--node-type t3a.medium \
--nodes 3 \
--nodes-min 1 \
--nodes-max 4 \
--node-ami auto \
--ssh-public-key ~/.ssh/id_xke_k8s_service.pub \
--node-private-networking

aws eks --region eu-west-1 update-kubeconfig --name xke-k8s-service
```

### Install ingress controller with Helm 3
kubectl create namespace infra
helm install --namespace infra nginx-ingress stable/nginx-ingress
