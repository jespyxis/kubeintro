You can create a custom image based n an existing image. To do so, you put the necessary instructions in a file called *Dockerfile* and you use an utiity to build the image.

We wil be using *docker build* because we don't have *buildx* installed in the lab environment. 

### **Common Dockerfile instructions**


| Instruction           | Meaning                                                               |
| --------------------- | --------------------------------------------------------------------- |
| FROM                  | It is the first instruction in the Dockerfile. Initializes the image based on an existing image   |
| WORKDIR               | Sets the working directory for any RUN, CMD, ENTRYPOINT, COPY, and ADD instructions that follow in the Dockerfile   |
| COPY                  | Copies new files or directories from the host filesystem to the filesystem of the container into the provided path   |
| ADD                   | Similar to COPY but can use URLs as input and can auto-extract ompressed files   |
| RUN                   | Executes any commands in a new layer on top of the current image and commits the results. The committed image will be used for the next step in the Dockerfile.   |
| CMD                   | Sets the default command to be executed when running the container.    |
| EXPOSE                | Makes a port available to outside the container    |

### **Create a custom image**

We are going to create a custom docker image and use it to create a container that runs a python app. 

#### 1. Setup the project folder and files

Create the project folder and go there

```
mkdir my-docker-project
cd my-docker-project
```{{exec}}

Create the requirements.txt and the app.py files

```
awk '/EOF/{exit} 1' > requirements.txt
Flask
EOF
```

```
awk '/EOF/{exit} 1' > app.py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "I see trees of green, red roses too"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
EOF
```

Create the Dockerfile

```
awk '/EOF/{exit} 1' > Dockerfile
FROM python:3.8-slim-buster
WORKDIR /app
COPY . /app
RUN pip install --no-cache-dir -r requirements.txt
EXPOSE 80
CMD ["python", "app.py"]

```{{exec}}


| Instruction                 | Explanation                                                           |
| --------------------------- | --------------------------------------------------------------------- |
| FROM python:3.8-slim-buster | Initializes the imaged based on a Python 3.8 image   |
| WORKDIR /app                | Sets the working directory for the app inside the container   |
| COPY . /app                 | Copies the application files from the host   |
| RUN pip install ...         | Installs Flask   |
| EXPOSE 80                   | Makes port 80 available outside the container   |
| CMD ["python", "app.py"]    | Sets the command that will run when you start the container   |




