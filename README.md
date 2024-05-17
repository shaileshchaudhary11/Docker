# DOCKER
## Dockerfile

A `Dockerfile` is a script consisting of a set of instructions on how to build a Docker image. It automates the process of creating a Docker image, specifying everything needed for the application to run. This includes the base image, application code, dependencies, environment variables, and commands to execute.

### Uses of a Dockerfile

1. **Consistency**: Ensures that the environment in which your application runs is consistent across different stages (development, testing, production).
2. **Automation**: Automates the creation of Docker images, making it easy to reproduce the environment.
3. **Version Control**: Dockerfiles can be version-controlled along with your application code, enabling you to track changes to your environment setup.
4. **Portability**: Makes it easy to share your application with others. They can build the image from the Dockerfile and run it in their own environment.

### Example of a Dockerfile

Here’s a simple example of a Dockerfile for a Python application:

```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```
### Explanation of the Dockerfile Instructions

- **FROM**: Specifies the base image to use. In this case, it's `python:3.8-slim`.
- **WORKDIR**: Sets the working directory inside the container to `/app`.
- **COPY**: Copies the current directory (where the Dockerfile is located) to the `/app` directory inside the container.
- **RUN**: Executes a command in the container. Here, it installs the Python dependencies listed in `requirements.txt`.
- **EXPOSE**: Informs Docker that the container listens on port 80 at runtime.
- **ENV**: Sets an environment variable `NAME` with the value `World`.
- **CMD**: Specifies the command to run within the container when it starts. In this case, it runs the Python script `app.py`.


### Building and Running the Docker Image

To build and run a Docker image from this Dockerfile, you would use the following commands:

1. **Build the Docker Image**

```sh
docker build -t my-python-app .
```
2. **Run the Docker Container**
```sh
docker run -p 4000:80 my-python-app
```  
This command maps port 4000 on your host to port 80 in the container, allowing you to access the application via http://localhost:4000.

## Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications. It allows you to use a YAML file to configure the services, networks, and volumes required for your application to run. With Docker Compose, you can define a multi-container application in a single file, making it easy to manage complex deployments.

### Uses of Docker Compose

1. **Orchestration**: Docker Compose simplifies the process of orchestrating multiple containers that make up an application, allowing you to define and run them together.
2. **Environment Management**: It provides a consistent environment across different stages of development, testing, and production.
3. **Service Configuration**: Docker Compose allows you to configure services, networks, and volumes in a declarative manner, making it easy to manage complex setups.
4. **Dependency Management**: You can specify dependencies between services and ensure they start up in the correct order.
5. **Portability**: Docker Compose files can be shared and used to deploy applications in different environments with minimal changes.

### Example of a Docker Compose File

Here's an example of a Docker Compose file (`docker-compose.yml`) for a simple web application with two services: a web server and a database.

```yaml
version: '3'

services:
  web:
    image: nginx:latest
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    depends_on:
      - db

  db:
    image: mysql:latest
    environment:
      MYSQL_ROOT_PASSWORD: example
      MYSQL_DATABASE: myapp
```

### Explanation of the Docker Compose File

- **version**: Specifies the version of the Docker Compose file format being used. In this case, it's version 3.
- **services**: Defines the services that make up the application.
  - **web**: Configuration for the web server service.
    - **image**: Specifies the Docker image to use for the web server (in this case, nginx:latest).
    - **ports**: Maps port 8080 on the host to port 80 on the container.
    - **volumes**: Mounts the `./html` directory on the host to `/usr/share/nginx/html` in the container.
    - **depends_on**: Specifies that the `web` service depends on the `db` service.
  - **db**: Configuration for the database service.
    - **image**: Specifies the Docker image to use for the database (in this case, mysql:latest).
    - **environment**: Sets environment variables required by the MySQL image.

### Running Docker Compose

To run the application defined in the Docker Compose file, you would use the following command:
```sh
docker-compose up
```
This command reads the `docker-compose.yml` file, creates the necessary Docker containers, networks, and volumes, and starts up the application.

### Conclusion
Docker Compose is a powerful tool for managing multi-container Docker applications, allowing you to define, configure, and run complex deployments with ease. By using a single YAML file to specify the services, networks, and volumes required for your application, you can streamline the development, testing, and deployment process


## Docker Commands

### Pull images from Docker Hub
```sh
docker pull <image_name>
```

### Run docker images
```sh
docker run -it <image_name>
```

### Make dockerfile and docker images

### Build docker images
```sh
docker build -t <tag_name> .
```
### Running image and making a container
```sh
docker run --name pc1 -it -d python
```
### Exercuting python container
```sh
docker exec -it ff3e13bac74e python
```

### List images
```sh
docker images
```

### List All Containers (Including Stopped)

```sh
docker ps -a
```

### Stop a Running Container
```sh
docker stop <container_id>
```
### Remove container
```sh
docker stop <container_id>
```
### Remove images
```sh
docker rmi <image_id>
```

### View Logs of a Container
```sh
docker logs <container_id>
```
### Start a Stopped Container
```sh
docker start <container_id>
```

### Restart a Running Container
```sh
docker restart <container_id>
```

### Pause a Running Container
```sh
docker pause <container_id>
```

### Run a Container with Volume Mount
```sh
docker run -v <host_directory>:<container_directory> <image_name>
```
