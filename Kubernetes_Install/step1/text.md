
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

and hold them to the current version. Putting the kubelet, kubeadm, and kubectl packages on hold is common practice. It is a measure to maintain cluster stability and control over the Kubernetes versions being used. When you're ready to upgrade Kubernetes, you can manually unhold the packages, upgrade them, and then put them back on hold if desired.

```
sudo apt-mark hold kubelet kubeadm kubectl
```{{exec}}

#### **2. Bootstrap the cluster**

Several cluster components will run in containers and we need to have the container images available. The kubeadm init command will pull the necessary images. However, for the sake of showing which images will be needed we will pull those images in advance. Execute the following command to pull the images:

```
kubeadm config images pull
```{{exec}}

List the obtained images

```
kubeadm config images list
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

Execute the following command to verify your cluster. You should have an one node cluster. Repeat the command until you see the node in READY status.

```
kubectl get nodes
```{{exec}}

Execute the *kubectl describe node* to check the node details

```
kubectl describe node ubuntu
```{{exec}}

Now, execute the following command to see which Pods were created


```
kubectl get pods --all-namespaces
```{{exec}}

#### **4. The Container Runtime Interface (CRI)**

CRI is a plugin interface that enables Kubernetes to use a wide variety of container runtimes, without the need to recompile. It was introduced to ensure a clear separation between the Kubernetes components (like the Kubelet) and the underlying container runtimes.

The Kubernetes community introduced CRI to decouple the Kubelet from specific container runtimes and provide a clear and stable API for container operations. 

The main components of CRI are:

| Component             | Description                                                               |
| --------------------- | --------------------------------------------------------------------- |
| ImageService          | Responsible for all image-related operations like pulling, removing, or inspecting images.     |
| RuntimeService        | Manages the complete lifecycle of the containers, from starting to stopping them, and includes operations like creating pods, updating container resources, or executing commands in containers.     |

The **cri-tools** package includes the **crictl** tool. You can use it as a command-line interface for CRI-compatible container runtimes.

Execute the following command to see which container images are available

```
crictl images
```{{exec}}

Execute the following command to obtain information about the running containers

```
crictl ps
```{{exec}}

Execute **crictl** without arguments or **critl --help** to check the available options. Feel free to play around with them.

#### **5. Adding Worker Nodes**

The next step would be to setup the worker nodes and make them join the cluster. On each worker node you would run 

```
kubeadm join [master-ip]:6443 --token [token] --discovery-token-ca-cert-hash [hash]
```
 to join the cluster. The exact command was actually listed by the *kubeadm init*.

### Congratulations! You finished the activity.














