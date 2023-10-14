There are several commands that can be used on **kubectl** in order to get information from the cluster:

| Command                       | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- |
| **kubectl api-resources**     | Check what kind of resources can be used in the cluster               |
| **kubectl explain**           | Obtain information about a particular resource type                   |
| **kubectl get**               | Obtain information about one or several resources in the cluster      |
| **kubectl version**           | Obtain the version for the client (kubectl) and the server (cluster)  |
| **kubectl describe**          | Obtain very detailed information for a particular resource            |
| **kubectl logs**              | Obtain the logs for a Pod or Container                                |

<br>

### **kubectl explain**

It provides documentation about Kubernetes API resources directly. Using it with the **recursive** option is a good way to understand the structure of a resource.

Let's obtain the structure of namespace API resources:

```
kubectl explain namespace --recursive
  ```{{exec}}

You can specify a particular location in the path and explain the structure from there as shown below:

```
kubectl explain pods.spec.containers.lifecycle --recursive
```{{exec}}

If you omit the **--recursive** option, it provides detailed explanation for the target field and subfields

```
kubectl explain pods.spec.containers.lifecycle
```{{exec}}


**kubectl get**

There are some techniques that are worth considering here. First of all, we can adjust the output by choosing exactly which columns we want to obtain. 

To do so, we need to know the path to each column that we want to include. Let's run an example:

```
kubectl get pod -A \
-o custom-columns=NAME:.metadata.name,\
NAMESPACE:.metadata.namespace,LABEL:.metadata.labels
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

**kubectl describe**

Provides detailed information about specific instances of resources that are currently running in your cluster. For each resource, it provides a comprehensive view of a resource, including its configuration, current state, and recent events. The information is formatted as a report to be easy to read.

You can use this command with or without specific resource identifiers. Let's try it out:

```
kubectl describe nodes
```{{exec}}

**kubectl logs**

This command can be used to obtain the log from a Pod or from a Container insider a Pod. Execute the command below to access the kube-scheduler log

```
kubectl logs kube-scheduler-controlplane \
        -c kube-scheduler -n kube-system
```{{exec}}

<details>
  <summary>Solution</summary>
  
  This content will be hidden until the summary is clicked.
</details>








