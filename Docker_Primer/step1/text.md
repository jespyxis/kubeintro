  You can use the *docker images* command to check which images are available in the local repository. Please try it now:
  ```
  docker images
  ```{{exec}}

You should not have any image so far

### **Downloading images from a repository**

The *docker pull* command downloads images from a Docker registry. 
  
The command has the following syntax: 

> docker pull [OPTIONS] NAME[:TAG|@DIGEST]

where: 

- OPTIONS are options to provide to *docker pull*. You can specify --all-tags to download all tagged images and --quiet to suppress verbose output
- NAME is the name of the image that you wand to download
- TAG provides the Tag for the image that you want to download. You can have several versions of an image under different Tags
- DIGEST provides an alternative way to identify the image that you want to download. Instead of providing the Tag you provide the Message Digest (SHA256 Hash)

By default, *docker pull* will get the images from Docker Hub. The NAME can be prefixed with the repository location if you want to use an alternate repository as in the example below

```
docker pull myregistry.example.com/myimage:latest
```

Execute the command to download the ubuntu image from Docker Hub

<details>
  <summary>Solution</summary>
  
  <br>
  You can execute the following command to download the ubuntu image from Docker Hub:

```
docker pull ubuntu
```{{exec}}

Because you provided no Tag it will download the latest version for the image.

</details>

Execute the *docker images* command again. This time you should find the ubuntu image

![docker images output](./docker_images.jpg)

### **Creating and running containers**

Execute the following command:

```
docker ps -a
```{{exec}}

This command will show all the created containers. The *-a* flag is used to show all containers and not only the ones that are currently running. 

You should not have any container created yet. Use the 

```
docker run --help
```

command to obtain Help information about the *docker run* command.

