### Docker Commands

### 1. Docker Login

Log in to Docker Hub using your Docker ID and password:

```bash

sudo docker login

```

Enter your Docker Hub credentials when prompted.

### 2. Create an Image

Assuming you have a Dockerfile in your current directory, you can build an image with:

```bash

sudo docker build -t my-image .

```

Replace `my-image` with your desired image name.

### 3. Run a Container

Run a container based on the image you created:

```bash

sudo docker run -d --name my-container my-image

```

Replace `my-container` with your desired container name.

### 4. Stop a Container

To stop a running container:

```bash

sudo docker stop my-container

```

Replace `my-container` with the name or ID of your container.

### 5. Delete a Container

To delete a stopped container:

```bash

sudo docker rm my-container

```

Replace `my-container` with the name or ID of your container.

### 6. Delete an Image

To delete an unused image:

```bash

sudo docker rmi my-image

```

Replace `my-image` with the name or ID of your image.

### 7. Docker Cleanup (Unused Containers and Images)

To remove all stopped containers:

```bash

sudo docker container prune

```

To remove all unused images:

```bash

sudo docker image prune

```

### 8. Docker Logout

Log out from Docker Hub:

```bash

sudo docker logout

```

### List Containers

To list all containers (running and stopped):

```bash

sudo docker ps -a

```

This command will display a list of all containers along with their details such as container ID, names, status, ports, and more.

### List Images

To list all images on your Docker host:

```bash

sudo docker images

```

This command will show a list of all Docker images available locally on your system, along with their repository, tag, image ID, and creation date.

### Additional Options

- To list only running containers, you can omit the `a` flag:
    
    ```bash
    
    sudo docker ps
    
    ```
    
- To list images with more detailed information including size, you can use the `a` flag:
    
    ```bash
    
    sudo docker images -a
    
    ```
    
