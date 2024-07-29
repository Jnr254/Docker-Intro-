#### Docker Commands and Practices

This document provides a comprehensive overview of essential Docker commands and practices, including running containers, managing images, and more. Use this as a quick reference guide for working with Docker.

#### System Configuration

Before running Docker containers, you might need to configure your system to ensure Docker works correctly. Use the following commands:

```bash
sudo sysctl -w kernel.apparmor_restrict_unprivileged_userns=0

sudo service docker stop
sudo service docker start
```

#### Basic Docker Commands

Here are some fundamental Docker commands you should be familiar with:

- **Run an Image:**
  ```bash
  docker run nginx
  ```

- **List Running Containers:**
  ```bash
  docker ps
  ```

- **List Previously and Currently Running Containers:**
  ```bash
  docker ps -a
  ```

- **Stop a Container:**
  ```bash
  docker stop <container-id>
  ```

- **Remove a Container:**
  ```bash
  docker rm <container-id>
  ```

- **Display the List of Images:**
  ```bash
  docker images
  ```

- **Remove an Image:**
  ```bash
  docker rmi <image-name>
  ```

- **Pull an Image:**
  ```bash
  docker pull <image-name>
  ```

#### Executing Commands on Running Containers

- **See the Contents of a File:**
  ```bash
  docker exec <container-id> <command>
  ```

- **Run a Container in the Background:**
  ```bash
  docker run -d kodekloud/simple-webapp
  ```

- **Run a Specific Tag of an Image:**
  ```bash
  docker run redis:4.0
  ```

- **Open Interactive Mode:**
  ```bash
  docker run -i <container-name>
  ```

- **Open Interactive Mode with Terminal:**
  ```bash
  docker run -it <image-name>
  ```

#### Port Mapping

Docker allows you to map container ports to the host machine. This is useful for accessing applications running in containers from outside the Docker network.

- **Port Mapping Example:**
  ```bash
  docker run -p 80:5000 <app-name>
  ```
  - Maps port 80 on the host to port 5000 in the container, allowing you to run multiple application instances by mapping different ports.

#### Volume Mapping

Volume mapping is essential for storing data from containers on the host machine. This ensures that data persists even if a container is deleted.

- **Inspect Data in a Container:**
  ```bash
  docker inspect <container-name>
  ```

- **View Container Logs:**
  ```bash
  docker logs <container-name>
  ```

#### Practice Exercises

**Exercise 1: Create a Redis Database Container**

Create a Redis database container called `redis` using the `redis:alpine` image.

```bash
docker run --name redis -d redis:alpine
```

**Exercise 2: Create a Click Counter Application**

Create a simple container called `clickcounter` using the `kodekloud/click-counter` image, link it to the Redis container, and expose it on host port 8085.

```bash
docker run -d --name=clickcounter --link redis:redis -p 8085:5000 kodekloud/click-counter
```

**Exercise 3: Access the Application**

You can now access this application using the Click-Counter tab above the terminal.

**Exercise 4: Clean Up Containers**

Delete the Redis and Click Counter containers.

```bash
docker rm -f redis clickcounter
```

**Exercise 5: Create a Docker Compose File**

Create a `docker-compose.yml` file under the directory `/root/clickcounter`. The compose file should have the following specifications:

- **Redis Service:**
  - Image: `redis:alpine`

- **Click Counter Service:**
  - Image: `kodekloud/click-counter`
  - Expose port 5000 on host port 8085

Once the file is created, run the following command:

```bash
docker-compose up
```

#### Creating Containers

Docker provides various options to create and manage containers. Here are some examples:

- **Create a Container Without a Tag:**
  ```bash
  docker container create hello-world
  ```

- **Create a Container With a Tag:**
  ```bash
  docker container create hello-world:linux
  ```

- **Sample Docker ID Example:**
  ```plaintext
  faa50845d20c55d3be9606f4c12773550fd8dc2de7f41ba8e5920d5d78078511
  ```

- **Start a Container:**
  ```bash
  docker container start faa50845d20c55d3be9606f4c12773550fd8dc2de7f41ba8e5920d5d78078511
  ```

- **Run a Container (Short Way):**
  ```bash
  docker run hello-world:linux
  ```

#### Building Docker Images

Docker images can be built using Dockerfiles. Here's how you can build images using Docker commands:

- **Build an Image:**
  ```bash
  docker build -t first-image './Exercise Files'/03_05/
  ```

- **Build an Image with a Specific Dockerfile:**
  ```bash
  docker build -t first-server -f './Exercise Files'/03_06/server.Dockerfile' './Exercise Files'/03_06/
  ```

- **Run the Built Image:**
  ```bash
  docker run -d first-server
  ```

#### Interactive Docker Commands

Docker supports executing commands interactively on running containers.

- **Execute Commands:**
  ```bash
  docker exec <container-id> date
  ```

- **Open Bash in a Container:**
  ```bash
  docker exec --interactive --tty <container-id> bash
  ```

- **Sample Output:**
  ```plaintext
  nobody@806942295d07:/$ #Output
  ```

- **Remove Containers and Stop Them from Running:**
  ```bash
  docker rm -f <container-id>
  ```

- **Display Docker IDs:**
  ```bash
  docker ps -aq
  ```

- **Delete All Containers at Once:**
  ```bash
  docker ps -aq | xargs docker rm
  ```

- **Remove an Image:**
  ```bash
  docker rmi <image-name>
  ```

- **Forcefully Remove an Image:**
  ```bash
  docker rmi -f <image-name>
  ```

- **Run a Container with a Name Assignment:**
  ```bash
  docker run -d --name web-server first-server
  ```

#### Port Binding

Port binding allows you to bind container ports to host ports, enabling access to containerized applications from the host.

- **Port Binding Example:**
  ```bash
  docker run -d --name web-server -p 5001:5000 first-server
  ```

#### Saving Data from Containers

You can save data from Docker containers to the host system to ensure data persistence.

---

This README.md provides a comprehensive overview of Docker commands, including practical examples and exercises. Use it as a reference guide for managing Docker containers and images effectively.

If you have any questions or need further assistance, feel free to reach out!
