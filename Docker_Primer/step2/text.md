You can create a custom image based n an existing image. To do so, you put the necessary instructions in a file called *Dockerfile* and you use an utiity to build the image.

We wil be using *docker build* because we don't have *buildx* installed in the lab environment. 

### *Common Dockerfile instructions*


| Instruction           | Meaning                                                               |
| --------------------- | --------------------------------------------------------------------- |
| FROM                  | It is the first instruction in the Dockerfile. Initializes the image based on an existing image   |
| WORKDIR               | Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY, and ADD instructions that follow in the Dockerfile   |
| COPY                  | Copies new files or directories from the host filesystem to the filesystem of the container into the provided path   |
| ADD                   | Similar to COPY but can use URLs as input and can auto-extract ompressed files   |
| RUN                   | Executes any commands in a new layer on top of the current image and commits the results. The committed image will be used for the next step in the Dockerfile.   |
| CMD                   | Sets the default command to be executed when running the container.    |
| ENTRYPOINT            | Sets the default command to be executed when running the container.    |


  ```
  docker images
  ```{{exec}}