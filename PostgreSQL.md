# PostgreSQL Docker Setup

This repository provides a simple setup for running a PostgreSQL 15 database using Docker. Follow the instructions below to pull the PostgreSQL image, start a PostgreSQL container, and verify that it's running.

## Prerequisites

- Docker installed on your machine. You can download it from [Docker's official website](https://www.docker.com/products/docker-desktop).

## Quick Start

### 1. Pull the PostgreSQL Docker Image

Run the following command to pull the PostgreSQL 15 image from Docker Hub:

```bash
docker pull postgres:15
```

### 2. Run the PostgreSQL Container

Execute the following command to start a PostgreSQL container. This command will set the PostgreSQL password for the postgres user, run the container in detached mode, and map port 5432 on your host to port 5432 in the container.

```bash
docker run --name postgres-container -e POSTGRES_PASSWORD=root -d -p 5432:5432 postgres:15
```

- `--name postgres-container`: Names the container `postgres-container`.
- `-e POSTGRES_PASSWORD=root`: Sets the PostgreSQL password for the `postgres` user to `root`.
- `-d`: Runs the container in detached mode.
- `-p 5432:5432`: Maps port 5432 on your host to port `5432` in the container.

### 3. Verify the Container is Running

To check if your PostgreSQL container is running, use:

```bash
docker ps
```

This command lists all running containers. You should see an entry for postgres-container if everything is set up correctly.

## Connecting to the PostgreSQL Container

You can connect to the PostgreSQL instance directly from within the Docker container using the psql client. This avoids the need to install PostgreSQL tools locally.

1. Start an Interactive Session with psql

Run the following command to start an interactive session with the psql client inside the container:

```bash
docker exec -it postgres-container psql -U postgres
```
- docker exec -it postgres-container: Start an interactive terminal session in the running container named postgres-container.
- psql: Run the psql client.
- -U postgres: Connect as the postgres user.

You will be connected to the PostgreSQL database, and you can start running SQL queries directly from this interactive session.

## Stopping and Removing the Container

To stop the running PostgreSQL container:

```bash
docker stop postgres-container
```

To remove the container:

```bash
docker rm postgres-container
```

## Troubleshooting

- Ensure Docker is running on your machine.
- Check container logs for errors using:

```bash
docker logs postgres-container
```

- Verify port mapping and firewall settings if you encounter connectivity issues.
