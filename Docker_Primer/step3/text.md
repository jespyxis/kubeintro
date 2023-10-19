

### **docker-compose**

You can use docker-compose to quickly define and run a multi-container application. docker-compose can be installed. If necessary, yu can get and install docker-compose from https://github.com/docker/compose. The following example illustrates this

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -	s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

**The docker-compose.yml file**

This file defines and describes the services, networks, and volumes for the Docker application. The table below lists some common used instructions

| Instruction           | Meaning                                                               |
| --------------------- | --------------------------------------------------------------------- |
| version               | Specifies the version of the docker-compose.yml format     |
| services              | Used to define the applicaton services. Each service will be running as a container   |
| build                 | For a service that needs a Dockerfile to build the custom image. It specifies the Dockerfile location   |
| image                 | For a service directly uses an image, identifies the image to use   |
| ports                 | Used to map between container and host ports   |
| volumes               | Used mount host paths or docker volumes   |
| environment           | Sets environment variables in the container   |
| networks              | Specifications for additional networks   |
| secrets               | Used to store sensitive data (e.g. tokes or passwords)   |
| configs               | Used to store configuration data outside of the services   |
| restart               | restart policy to apply to the services (e.g. restart on failure)   |



 Use the [more details](https://docs.docker.com/compose/compose-file/) link to see the complete documentation