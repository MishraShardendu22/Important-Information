## What is a Docker ?

### Docker is a platform that lets you package an application and its dependencies into a "container," which can run consistently on any system. 
### Think of it like a virtual box that has everything the app needs to run, so no matter where you put the box (your laptop, a server, etc.), the app works the same way.


## Command Example 
### PostgreSQL

To run a PostgreSQL container:

```bash
docker run --name postgres-container -e POSTGRES_PASSWORD=yourpassword -d -p 3001:5432 postgres:14
```

**Explanation:**

- `--name postgres-container`: Names the container "postgres-container."
- `-e POSTGRES_PASSWORD=yourpassword`: Sets the PostgreSQL user password (replace `yourpassword` with a secure password).
- `-d`: Runs the container in detached mode (in the background).
- `-p 3001:5432`: Maps port 5432 of the container to port 3001 on the host. Access PostgreSQL via `localhost:3001`.

### MongoDB

To run a MongoDB container:

```bash
docker run --name mongo-container -d -p 3002:27017 mongo:6.0
```

**Explanation:**

- `--name mongo-container`: Names the container "mongo-container."
- `-d`: Runs the container in detached mode.
- `-p 3002:27017`: Maps port 27017 of the container to port 3002 on the host. Access MongoDB via `localhost:3002`.

## Accessing the Databases

- **PostgreSQL**: Connect to `localhost:3001`.
- **MongoDB**: Connect to `localhost:3002`.

## Stopping and Removing Containers

To stop and remove the containers, use the following commands:

```bash
docker stop postgres-container
docker rm postgres-container
docker stop mongo-container
docker rm mongo-container
```

## Command Breakdown
```bash
docker run -d ^
  --name mongodb_container ^
  --net mongo_network ^
  -p 3000:8081 ^
  -e INTDB_ROOT_USERNAME=admin ^
  -e INTDB_ROOT_PASSWORD=admin_pass ^
  mongo
```

- `docker run -d`: This command starts a new container in detached mode (in the background). The `-d` flag ensures that the container runs independently of the terminal.

- `--name mongodb_container`: This option assigns a name (`mongodb_container`) to the container. You can use this name to refer to the container later instead of using its container ID.

- `--net mongo_network`: This specifies the network to which the container will be connected. In this case, it connects the container to a Docker network named `mongo_network`. 

- `-p 3000:8081`: This flag maps the container’s port `8081` to port `3000` on the host machine. Any traffic sent to `localhost:3000` on your host will be forwarded to the container's port `8081`.

- `-e INTDB_ROOT_USERNAME=admin`: This sets an environment variable (`INTDB_ROOT_USERNAME`) inside the container, specifying the root username for the MongoDB instance as `admin`.

- `-e INTDB_ROOT_PASSWORD=admin_pass`: This sets another environment variable (`INTDB_ROOT_PASSWORD`) for the MongoDB instance, defining the root password as `admin_pass`.
 
- `mongo`: This is the name of the Docker image to use. In this case, it pulls the official MongoDB image from Docker Hub and runs it.
