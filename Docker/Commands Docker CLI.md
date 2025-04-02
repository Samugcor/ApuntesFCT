
### Images

- **Download image:** Downloads  the latest version of an image from [[2_Quick Start#^794fbb|Docker Hub]]
  `docker pull <image-name>`

- **Download image version:** Downloads  the specified version of an image from [[2_Quick Start#^794fbb|Docker Hub]]
  `docker pull <image-name>:<image-version>`

### Run Containers

- **Docker run:** Run image generating a container
  `docker run <image-name>`

- **Docker run --name**: Runs an image generating a container with the given name
  `docker run --name <container-name> <image-name>`

- **Docker run interactive shell:** Run image generating an interactive shell for the container
  `docker run -it <image-name>`

> [!tip] 
> To exit this console and go back to the host machine (stopping the container) we enter: `exite`

- **Docker run detached:** Run image generating a container in the background, not communicating directly with our shell
  `docker run -d <image-name>`

### List

- **List images:** Shows a list of all the existing images in the machine
  `docker images`

- **List running containers**: Shows a list with information (id, image, status...) of the running containers
  `docker ps`

- **List filtered running containers**: Shows a list of the containers matching the filter
  `docker ps -f "name=<container-name>`

> [!info] 
> **-f** : in this case stands for **filter**

### Manage Images

- **Remove Images:**
  `docker image rm <image-name>

> [!warning] 
> You can only delete an image if there are no containers based on it 

- **Remove dangling Images:** Removes Dangling images (images that are not associated with any tag and are not referenced by any containers)[^1]
  `docker image prune

- **Remove unused Images:** Removes all unused images (images with no associated containers)
  `docker image prune -a

> [!info] 
> **-a** : in this case stands for **all**
### Manage Containers

-  **Stop container**:
   `docker stop <container-id>|<container-name>`

- **Remove container:**
  `docker container rm <container-id>`

- **Remove stopped containers:** Removes all stopped containers 
  `docker container prune

### Logs

- **Docker logs**: Shows the outputs of a container until that point
  `docker logs <container-id>`

- **Docker logs real time:** Shows the outputs of a container in real time
  `docker logs -f <container-id>`

> [!info] 
> **-f** : in this case stands for follow
> To exit press: **ctr + c**

---
[^1]: Dangling Images can occur when we re-use the name for another image. Usually this happens with images that we create and modify, because when modified they generate a new one.