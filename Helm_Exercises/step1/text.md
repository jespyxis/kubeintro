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
helm repo add --help
```{{exec}}

Click on the entry for the nginx Chart. You will see a small menu on the right

![Helm Chart Menu](./menu.jpg)

You can use the menu to access the Templates in the Chart, the default values in the values.yaml in the Chart and to obtain information on how to use the Chart to perform an installation. 

Click on the **Install** entry. It shows you how to add the Bitnami repository. For convenience, I copied the command here. Execute the command to add the Bitnami repository

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```{{exec}}
