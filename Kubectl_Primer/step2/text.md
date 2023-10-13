There are several commands that can be used on **kubectl** in order to get information from the cluster:

| Command                       | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- |
| **kubectl api-resources**     | Check what kind of resources can be used in the cluster               |
| **kubectl explain**           | Obtain information about a particular resource type                   |
| **kubectl get**               | Obtain information about one or several resources in the cluster      |
| **kubectl verson**            | Obtain the version for the client (kubectl) and the server (cluster)  |
| **kubectl describe**          | Obtain very detailed information for a particular resource            |
| **kubectl logs**              | Obtain the logs for a Pod or Container                                |

<br>

**kubectl explain**

It provides documentation about Kubernetes API resources directly. Using it with the **recursive** option is a good way to understand the structure of a resource.

Let's obtain the structure of namespace API resources:

```
kubectl explain pnamespace --recursive
  ```{{exec}}

**kubectl get**

There are some techniques that are worth considering here. First of all, we can adjust the output by choosing exactly which columns we want to obtain. 

To do so, we need to know the path to each column that we want to include. Let's run an example:

```
kubectl get pod -A \
-o custom-columns=NAME:.metadata.name,NAMESPACE:.metadata.namespace,LABEL:.metadata.labels
  ```{{exec}}

You can also use the **-w** flag to keep listening and wait for changes on resources. Let's illustrate this. Execute the following command:

```
kubectl get namespaces -w
```{{exec}}

Now, click on the **+** button at the right of Tab1 in order to open a new Tab. Then, move to that Tab and execute the following command:

```
kubectl create namespace myownnamespace
```{{exec}}

Return to **Tab1**. Your new namespace should appear because the command was still listening for changes.





