
We will install kubernetes and setup a single node cluster. 

Start by turning swap off as it is not supported by Kubernetes

```
sudo swapoff -a
```{{exec}}

#### **1. Install the required packages**

Then, we add the Kubernetes official apt repository

```
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
```{{exec}}

Install the required packages 

```
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
```{{exec}}

and hold them to the current version

```
sudo apt-mark hold kubelet kubeadm kubectl
```{{exec}}

#### **2. Bootstrap the cluster**

Execute this command to initialize the cluster. The command usually ends with a kubeadm join command with tokens and IP that you will need to use on worker nodes to join the cluster.

```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --ignore-preflight-errors=numCPU
```{{exec}}

Move the kubeconfig file to its default location and give it the appropriate permissions:

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```{{exec}}

#### **3. Setup the pod network**

A pod network is a way for pods to communicate with each other. Execute the following command to setup a Flannel Pod network

```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```{{exec}}

#### **4. Verify the cluster**

Execute the following command to verify your cluster. You should have an one node cluster

```
kubectl get nodes
```{{exec}}











