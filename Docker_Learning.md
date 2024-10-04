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
  -e INTDB_SERVER=mongodb_container ^
  mongo
```


1. **`docker run -d`**: 
   - This command starts a new container in detached mode (`-d`), meaning it runs in the background.

2. **`--name mongodb_container`**: 
   - This assigns the name `mongodb_container` to the container, making it easier to reference later.

3. **`--net mongo_network`**: 
   - This connects the container to a Docker network called `mongo_network`. This is useful for container communication.

4. **`-p 3000:8081`**: 
   - This maps port `8081` of the container to port `3000` on the host machine. You can access MongoDB through port `3000` on your local machine.

5. **`-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin`**: 
   - This sets an environment variable for the MongoDB admin username. In this case, it’s set to `admin`.

6. **`-e ME_CONFIG_MONGODB_ADMINPASSWORD=admin_pass`**: 
   - This sets another environment variable for the admin password, which is `admin_pass`.

7. **`-e ME_CONFIG_MONGODB_SERVER=mongodb_container`**: 
   - This specifies the MongoDB server address, which is the name of the container itself (`mongodb_container`).

8. **`mongo`**: 
   - This specifies the image to use, in this case, the official MongoDB image.

### Summary:
This command sets up a MongoDB container that can be accessed from your local machine via port `3000`. It also configures an admin username and password for accessing the database. The container is part of a specified Docker network, which allows for easy communication with other containers in that network.
