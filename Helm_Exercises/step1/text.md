We will start by installing Helm in the current node

Execute the following command to install Helm:

```
sudo snap install helm --classic
```{{exec}}

Execute the following command to check the Helm version. You should be using Helm 3.

```
helm version
```{{exec}}

Create a new namespace that we are going to use in our exercises

```
kubectl create namespace helm-exercises
```{{exec}}

Change the Helm environment to use this namespace. We start by checking the current namespace

```
helm env | grep NAMESPACE
```{{exec}}

Then, execute the following command to change it to our helm-exercises namespace

```
export HELM_NAMESPACE=helm-exercises
```{{exec}}


Go to the [Artifact Hub site](https://artifacthub.io) and search for nginx. One of the entries shows that the Chart is available in the Bitnami repository. 

Execute the following command to check the syntax of the helm add repo command

```
helm add repo --help
```{{exec}}

Use the obtained information to add the Bitnami repository. Name it bitnami