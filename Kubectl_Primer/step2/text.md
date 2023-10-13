There are several commands that can be used on **kubectl** in order to get information from the cluster:

| Command                       | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- |
| **kubectl api-resources**     | Check what kind of resources can be used in the cluster               |
| **kubectl get**               | Obtain information about one or several resources in the cluster      |
| **kubectl explain**           | Obtain information about a particular resource type                   |
| **kubectl verson**            | Obtain the version for the client (kubectl) and the server (cluster)  |
| **kubectl describe**          | Obtain very detailed information for a particular resource            |
| **kubectl logs**              | Obtain the logs for a Pod or Container                                |

###kubectl get

There are some techniques that are worth considering here. First of all, we can adjust the output by choosing exactly which columns we want to obtain. 

To do so, we need to know the path to each column that we want to include. Let's run an example:

```
kubelet get pod -A -o custom-columns=NAME:.metadata.name,NAMESPACE:.metadata.namespace,LABEL:.metadata.labels
  ```{{exec}}



