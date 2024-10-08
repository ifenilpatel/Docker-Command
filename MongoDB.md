# MongoDB Docker Setup

This repository provides a simple setup for running a MongoDB 6.0 database using Docker. Follow the instructions below to pull the MongoDB image, start a MongoDB container, and verify that it's running.

## Prerequisites

- Docker installed on your machine. You can download it from [Docker's official website](https://www.docker.com/products/docker-desktop).

## Quick Start

### 1. Pull the MongoDB Docker Image

Run the following command to pull the MongoDB 6.0 image from Docker Hub:

```bash
docker pull mongo:6.0
```

### 2. Run the MongoDB Container

Execute the following command to start a MongoDB container. This command will set the MongoDB root username and password, run the container in detached mode, and map port 27017 on your host to port 27017 in the container.

```bash
docker run --name mongo-container -e MONGO_INITDB_ROOT_USERNAME=root -e MONGO_INITDB_ROOT_PASSWORD=root -d -p 27017:27017 mongo:6.0
```

- `--name mongo-container`: Names the container `mongo-container`.
- `-e MONGO_INITDB_ROOT_USERNAME=root`: Sets the MongoDB root username to `root`.
- `-e MONGO_INITDB_ROOT_PASSWORD=root`: Sets the MongoDB root password to `root`.
- `-d`: Runs the container in detached mode.
- `-p 27017:27017`: Maps port 27017 on your host to port `27017` in the container.

### 3. Verify the Container is Running

To check if your MongoDB container is running, use:

```bash
docker ps
```

This command lists all running containers. You should see an entry for mongo-container if everything is set up correctly.

## Connecting to the MongoDB Container

You can connect to the MongoDB instance using the mongosh shell directly from within the Docker container. This avoids the need to install any MongoDB tools locally.

1. Access the MongoDB Shell

For example, using the mongo command-line tool:

Run the following command to start an interactive session with the MongoDB shell (mongosh) inside the container:

```bash
docker exec -it mongo-container mongosh -u root -p root --authenticationDatabase admin
```
- `docker exec -it mongo-container`: Start an interactive terminal session in the running container named `mongo-container`.
- `mongosh`: Run the MongoDB Shell.
- `-u root -p rootpassword`: Specify the MongoDB username and password.
- `--authenticationDatabase admin`: Specify the database to authenticate against.

## Stopping and Removing the Container

To stop the running MongoDB container:

```bash
docker stop mongo-container
```

To remove the container:

```bash
docker rm mongo-container
```

## Troubleshooting

- Ensure Docker is running on your machine.
- Check container logs for errors using:

```bash
docker logs mongo-container
```

- Verify port mapping and firewall settings if you encounter connectivity issues.
