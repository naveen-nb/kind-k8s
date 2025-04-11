# kind-k8s
Exploring local K8s clusters

### Verify Docker in the system
docker --version

### Install kind on Ubuntu
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.27.0/kind-linux-amd64  
chmod +x ./kind  
sudo mv ./kind /usr/local/bin/kind

Other OS/Distros can refer to the documentation here:
https://kind.sigs.k8s.io/docs/user/quick-start/#installation

### Verify kind installation
kind --version

### Login to docker if not already done
docker login

### Simple single node cluster creation
kind create cluster -n simple-cluster

### Multi node cluster creation
kind create cluster --config multi-node-cluster.yml

### Verify the cluster creation
kind get clusters

### Verify if Kubectl is pointing to the newly created cluster
kubectl config current-context  # If already set, continue. Else, run next line  
kubectl config set-context kind-<cluster_name>  # In our case, its simple-cluster

### Details of the cluster
kubectl cluster-info --context kind-<cluster_name>

### Deploy a simple nginx image
kubectl create deployment nginx-demo --image=nginx

### Verify the pods
kubectl get pods

### Test port-forwarding to access the running nginx
kubectl port-forward pod/<nginx_pod_name> 8080:80

### Verify nginx-server is up and running
If docker on local windows/mac - http://localhost:8080  
If docker on linux - curl http://localhost:8080

### Delete the cluster
kubectl delete cluster -n simple-cluster
