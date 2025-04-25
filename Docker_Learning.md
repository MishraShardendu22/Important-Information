## What is a Docker ?

### Docker is a platform that lets you package an application and its dependencies into a "container," which can run consistently on any system. 
### Think of it like a virtual box that has everything the app needs to run, so no matter where you put the box (your laptop, a server, etc.), the app works the same way.



# Breakdown of : 
`docker run --name postgres-container -e POSTGRES_PASSWORD=yourpassword -d -p 3001:5432 postgres:14`
`docker run --name mongo-container -d -p 3002:27017 mongo:6.0`


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
