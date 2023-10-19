
We will install kubernetes and setup a single node cluster. 

Start by turning swap off as it is not supported by Kubernetes

```
sudo swapoff -a
```{{exec}}

#### **1. Install the required packages**

Then, we add the Kubernetes official apt repository

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```{{exec}}

```
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

Several cluster components will run in containers and we need to have the container images available. The kubeadm init command will pull the necessary images. However, for the sake of showing which images will be needed we will pull those images in advance. Execute the following command to pull the images:

```
kubeadm config images pull
```{{exec}}

Now, execute the *kubeadm init* command to initialize the cluster. The command usually ends with a kubeadm join command with tokens and IP that you will need to use on worker nodes to join the cluster.

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

Execute the *kubectl describe node* to check the node details

```
kubectl get nodes
```{{exec}}

Now, execute the following command to see which Pods were created


```
kubectl get pods --all-namespaces
```{{exec}}

#### **4. Next steps**

the next step would be to setup the worker nodes and make them join the cluster. On each worker node you would run 

```
kubeadm join [master-ip]:6443 --token [token] --discovery-token-ca-cert-hash [hash]
```
 to join the cluster. The exact command was actually listed by the *kubeadm init*.


### Congratulations! You finished the activity.














