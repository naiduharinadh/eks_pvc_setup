create cluster in eks: <br />
`  eksctl create cluster -f cluster1.yml `
<br />
get the role ID from here toattach IAM policies: <br />
` kubectl get -n kube-system configmap/aws-auth -o yaml ` <br />
install the CSI-EBS driver: <br />
` kubectl apply -k "github.com/kubernetes-sigs/aws-ebs-csi-driver/deploy/kubernetes/overlays/stable/?ref=release-1.28" ` <br />
<br />
add the nodegroups to the existed cluster: <br />
` eksctl create --name k8s_cluster_1 --version 1.29 --nodegroup-name nodeGroupDemo  --nodes 2 --nodes-min 2 --ssh-access --nodes-max 3 --instance-name k8s_slaves --enable-ssm --instance-types t2.micro `
<br /> 
create deployment POD: <br/>
`kubectl create deployment myweb --image=harinadh14/nodeapp:v1.0 `
<br />
expose the container exposed port with EBS port  to connect cnt from outside : <br />
 ` kubectl expose deployment myweb --name=mylbsvc2 --port=2323 --target-port=4623 --type=LoadBalancer `
