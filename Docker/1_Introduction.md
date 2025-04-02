---
aliases:
  - Docker
---
### What is Docker?

**Docker** is a platform used for developing, shipping, and running applications inside **containers**. Containers are lightweight, portable, and isolated environments that include everything an application needs to run: code, runtime, libraries, and dependencies. Docker helps you create these containers and manage them easily.

### What is Docker used for?

Docker is primarily used for:

- **Containerization**: It packages applications and all their dependencies into containers, ensuring consistency across different environments (development, testing, production).

- **[[Microservices]]**: Docker is often used in microservices architectures, where different parts of an application (services) are packaged into separate containers and interact with each other.

- **Simplified Deployment**: Docker makes deploying applications much easier by ensuring that the environment is the same everywhere (your local machine, staging, production, etc.).

- **Isolation**: Each container runs its own set of processes, independent of others, so it won't interfere with other applications running on the same host.

- **CI/CD**: Docker is widely used in Continuous Integration and Continuous Deployment pipelines for automating the testing and deployment of applications.

### How does Docker work?

Docker works by creating a **Docker container** which is essentially a process that runs on a host operating system but is isolated from other processes. Here's a simplified breakdown of how it works:

- **Docker Images**: Docker images are the blueprints or templates from which containers are created. These images contain everything needed to run an application, including the operating system libraries, dependencies, and the application itself.

- **Docker Containers**: Containers are instances of images. When you run a Docker container, it’s essentially a running instance of an image. Containers share the host system's kernel, but they have their own isolated filesystem, memory, and network.

- **Docker Engine**: This is the core component of Docker. It’s responsible for managing Docker containers, images, and networks. It can run on Linux, Windows, or macOS, and it interacts with the Docker daemon to run and manage containers.

- **Docker Registry**: A registry is a collection of Docker images. Docker Hub is the most commonly used public registry, but you can set up your own private registry.