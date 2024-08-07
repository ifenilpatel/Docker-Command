# MySQL Docker Setup

This repository provides a simple setup for running a MySQL 8.0 database using Docker. Follow the instructions below to pull the MySQL image, start a MySQL container, and verify that it's running.

## Prerequisites

- Docker installed on your machine. You can download it from [Docker's official website](https://www.docker.com/products/docker-desktop).

## Quick Start

### 1. Pull the MySQL Docker Image

Run the following command to pull the MySQL 8.0 image from Docker Hub:

```bash
docker pull mysql:8.0
```

### 2. Run the MySQL Container

Execute the following command to start a MySQL container. This command will set the root password to root, run the container in detached mode, and map port 3306 on your host to port 3306 in the container.

```bash
docker run --name mysql-container -e MYSQL_ROOT_PASSWORD=root -d -p 3306:3306 mysql:8.0
```

- `--name mysql-container`: Names the container `mysql-container`.
- `-e MYSQL_ROOT_PASSWORD=root`: Sets the root password to `root`.
- `-d`: Runs the container in detached mode.
- `-p 3306:3306`: Maps port 3306 on your host to port `3306` in the container.

### 3. Verify the Container is Running

To check if your MySQL container is running, use:

```bash
docker ps
```

This command lists all running containers. You should see an entry for mysql-container if everything is set up correctly.

## Connecting to the MySQL Container

You can connect to the MySQL instance directly from within the Docker container using the MySQL client.

1. Start an Interactive Session with MySQL Client
   
Run the following command to start an interactive session with the MySQL client (mysql) inside the container:

```bash
docker exec -it mysql-container mysql -u root -p
```
- `docker exec -it mysql-container`: Start an interactive terminal session in the running container named `mysql-container`.
- `mysql`: Run the MySQL client.
- `-u root`: Specify the MySQL username (root).
- `-p`: Prompt for the password.

You will be prompted to enter the root password (root). After entering the password, you’ll be in the MySQL interactive shell where you can run SQL queries.

## Stopping and Removing the Container

To stop the running MySQL container:

```bash
docker stop mysql-container
```

To remove the container:

```bash
docker rm mysql-container
```

## Troubleshooting

- Ensure Docker is running on your machine.
- Check container logs for errors using:

```bash
docker logs mysql-container
```

- Verify port mapping and firewall settings if you encounter connectivity issues.
