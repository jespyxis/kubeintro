  You can call **kubectl** without arguments. If you do so, it provides you the **kubectl** global help. This gives you an explanation of the several kubectl commands and their categories.

  Try it now:

  ```
  kubectl
  ```{{exec}}

  The output of the command shows you all the commands that you can use in kubectl and their categories. OpenShift has a CLI tool that is similar to kubectl. It is named **oc**

  Now, try to execute the following command:

  ```
  kubectl version
  ```{{exec}}

  This command is used to display the version information of both the kubectl command-line tool (client-version) and the Kubernetes cluster it's connected to (server-version). Because the command don't require any additional option, it executes and provides you with the desired data.

  Now, try the following command:

  ```
  kubectl get
  ```{{exec}}

  What happened this time? The **kubectl get** command doesn't have enough information to execute. As a result, it prints out to you some instructions:

  - How to get help about the **kubectl get** command
  - How to get information on the resource types that you can use

  Let's try to get help on the command. Execute:

  ```
  kubectl get -h
  ```{{exec}}

  The **kubectl api-resources** command provides information about all the possible API resources in your kubernetes cluster. Let's try it out:

  ```
  kubectl api-resources
  ```{{exec}}

  Some resources have alternative shornames that you can use with kubectl. Those are listed under *shortnames*. For example, a *configmap* can also be used using the *cm* shortname.

  Some resources are scoped to _namespaces_ while others are not. If a resource belongs to a namespace, you must either provide the namespace or say that you want to use the kubectl command for all namespaces.


