

### **docker-compose**

You can use docker-compose to quickly define and run a multi-container application. docker-compose can be installed. If necessary, yu can get and install docker-compose from https://github.com/docker/compose. The following example illustrates this

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
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

 **Building the example**

 We will build a simple Flask application that uses Redis for the data. 
 
 A bind volume is created that mounts the local app directory to the /app directory inside the container. This ensures that changes made to the Flask application on the host machine are immediately reflected inside the container.

 A named volume redis-data is defined to persist the Redis data. This volume is mounted to the /data directory inside the Redis container, which is where Redis stores its data by default.

 #### **1. Creating the project folder and files**

 Execute 

```
mkdir flask_redis_app
cd flask_redis_app
```{{exec}}

to create the project folder

Create the **app.py** file with the following content

```
from flask import Flask
import redis

app = Flask(__name__)
redis_client = redis.StrictRedis(host='redis', port=6379, db=0)

@app.route('/')
def hello():
    redis_client.incr('hits')
    return 'Hello! This page has been viewed %s times.' % redis_client.get('hits').decode('utf-8')

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```{{copy}}

Create the **requirements.txt** file with the following content

```
Flask==2.0.2
redis==3.5.3
```{{copy}}

Create the **docker-compose.yml** file with the following content

```
version: '3.7'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - ./app:/app  # Mounts the Flask application code into the container
    depends_on:
      - redis

  redis:
    image: "redis:latest"
    volumes:
      - redis-data:/data  # Mounts a named volume to persist Redis data

volumes:
  redis-data:  # Named volume for Redis data
```{{copy}}

 #### **2. Build and run the example**

 Use the following commands to build and run the application

```
docker-compose build
docker-compose up
```{{exec}}

Use the [following link]({{TRAFFIC_HOST1_5000}})
 to access the application:







