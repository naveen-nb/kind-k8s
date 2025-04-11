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

### Verify the cluster creation
kind get clusters

### Verify if Kubectl is pointing to the newly created cluster
kubectl config current-context  # If already set, continue. Else, run next line
kubectl config set-context kind-<cluster_name>  # In our case, its simple-cluster

### Details of the cluster
kubectl cluster-info --context kind-<cluster_name>

### Delete the cluster
kubectl delete cluster -n simple-cluster
