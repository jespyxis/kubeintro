You can call kubectl without arguments. If you do so, it provides you the kubectl global help. This gives you an explanation of the several kubectl commands and their categories.

Try it now:

kubectl
```{{exec}}

The output of the command shows you all the commands that you can use in kubectl and their categories. OpenShift has a CLI tool that is similar to kubectl. It is named **oc**

Now, try to execute the following command:

kubectl version


This command is used to display the version information of both the kubectl command-line tool (client-version) and the Kubernetes cluster it's connected to (server-version). Because the command don't require any additional option, it executes and provides you with the desired data.

Now, try the following command:

kubectl get


What happened this time? The **kubectl get** command doesn't have enough information to execute. As a result, it prints out to you some instructions:

- How to get help about the **kubectl get** command
- How to get information on the resource types that you can use

Let's try to get help on the command. Execute:

kubectl get -h


The **kubectl api-resources** command provides information about all the possible API resources in your kubernetes cluster. Let's try it out:

kubectl api-resources


Some resources have alternative short names that you can use with kubectl. Those are listed under *shortnames*. For example, a *configmap* can also be used using the *cm* shortname.

Some resources are scoped to _namespaces_ while others are not. If a resource belongs to a namespace, you must either provide the namespace or say that you want to use the kubectl command for all namespaces.

Now that you know which resources are out there, let's use that knowledge. We are going to complete the **kubectl get** command to obtain information about the nodes of the cluster. Execute:

kubectl get nodes


The command presents some summary information about the Kubernetes cluster nodes.

Now, execute the command that will provide you the options that you can use with **kubectl get nodes**. One of the options, **-o** allows you to choose between several output types. Try the following:

kubectl get nodes -o wide


This is very useful as several get commands will only output basic information if you invoke them without **-o wide**. 

Open anothet tab by clicking o the **+** button at the right of **Tab 1**. Got to this tab and execute:

kubectl get nodes -o yaml


What did you get this time? The **kubectl get** command provided you the complete specification and status information for each of the nodes in YAML format.

There are several options that are common to all kubectl commands. To see those options, run the following command:

kubectl options



### Congratulations! You finished the first step.

