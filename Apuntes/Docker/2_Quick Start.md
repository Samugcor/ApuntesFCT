#apuntes #docker #quickstart 
___
### 1. **Install Docker**

- For most systems, you can install Docker by following the official guide: [Docker Install](https://docs.docker.com/desktop/setup/install/windows-install/)
- También puedes instalarlo mediante comandos: [Docker Install from the command line](https://docs.docker.com/desktop/setup/install/windows-install/#:~:text=to%20take%20effect.-,Install%20from%20the%20command%20line,-After%20downloading)
- Once installed, you can verify by running `docker --version` in your terminal

### 2. **Using Docker** 

Docker can be used with it's graphic interface [[Docker Desktop]] or by command lines with 
[[Docker CLI]]
### 3. **Running Docker Containers**

- **Docker Pull**: First, you can pull an image from [Docker Hub](https://hub.docker.com/)[^1].
  `docker pull hello-world`

	This will download a simple image for testing.

- **Docker Run**: Next, you can run the container.
  `docker run hello-world`

    This will run the image and print a message saying "Hello from Docker!"

### 4. **Creating Docker Images**

You can create a Docker image by defining a `Dockerfile`, which is a script that specifies how to build an image. Here's an example `Dockerfile`:

```
# Use a base image 
FROM node:14  

# Set working directory 
WORKDIR /app  

# Copy files to container 
COPY . .  

# Install dependencies 
RUN npm install  

# Expose port 
EXPOSE 3000  

# Run the application 
CMD ["npm", "start"]
```

You build the image using the `docker build` command:
`docker build -t my-app .`

This creates an image called `my-app` based on the instructions in your `Dockerfile`.

### 5. **Managing Containers**

- **List running containers**:
  `docker ps`

- **Stop a running container**:
  `docker stop <container_id>`

- **Remove a container**:
   `docker rm <container_id>`

- **List all containers (running and stopped)**:
  `docker ps -a`

### 6. **Docker Compose**

For more complex applications with multiple containers, Docker Compose helps you define and run multi-container applications. You can define the services, networks, and volumes in a `docker-compose.yml` file, like this:

```yaml
version: '3'
services:   
	web:     
		image: nginx     
		ports:       
			- "8080:80"   
	db:     
		image: postgres     
		environment:       
			POSTGRES_PASSWORD: example
```

To run the application:

```bash
docker-compose up
```


---
[^1]: **Docker Hub** is a registry of docker images made by other users

^794fbb
