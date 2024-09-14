# Redis Docker Guide

## 1. How to Install Redis

To install Redis using Docker, use the following command:

```bash
docker pull redis
```

This command pulls the latest Redis image from the Docker Hub repository.

## 2. How to Expose Port

By default, Redis runs on port 6379. To expose this port when running the Redis container, use the `-p` flag in the `docker run` command. For example:

```bash
docker run --name my-redis -p 6379:6379 redis
```

This maps port 6379 of the container to port 6379 on your host machine.

## 3. How to Start Interactive

To start a Redis container in interactive mode with a terminal session, use the following command:

```bash
docker run -it --name my-redis -p 6379:6379 redis redis-cli
```

This command will start the Redis container and open an interactive `redis-cli` session.

## 4. How to Use CLI

To use the Redis CLI tool, you can either run it directly in the container or use it from your host machine if you have `redis-cli` installed. To access the Redis CLI in a running container, use:

```bash
docker exec -it my-redis redis-cli
```

Once in the CLI, you can issue Redis commands like `SET`, `GET`, `DEL`, etc.

## 5. Commands Cheat for Node.js

When working with Redis in a Node.js environment, you will typically use the `ioredis` or `redis` package. Here are some common commands:

### Read Commands

- **Get a value by key**:

  ```javascript
  redis.get("key").then((value) => console.log(value));
  ```

- **Get multiple values by keys**:

  ```javascript
  redis.mget(["key1", "key2"]).then((values) => console.log(values));
  ```

- **Get all members of a set**:

  ```javascript
  redis.smembers("set").then((members) => console.log(members));
  ```

- **Get all fields and values of a hash**:
  ```javascript
  redis.hgetall("hash").then((fields) => console.log(fields));
  ```

### Write Commands

- **Set a key-value pair**:

  ```javascript
  redis.set("key", "value");
  ```

- **Add a member to a set**:

  ```javascript
  redis.sadd("set", "member");
  ```

- **Push an element to a list**:

  ```javascript
  redis.rpush("list", "value");
  ```

- **Set a field in a hash**:
  ```javascript
  redis.hset("hash", "field", "value");
  ```

### Delete Commands

- **Delete a key**:

  ```javascript
  redis.del("key");
  ```

- **Remove a member from a set**:

  ```javascript
  redis.srem("set", "member");
  ```

- **Pop an element from a list**:
  ```javascript
  redis.lpop("list").then((value) => console.log(value));
  ```

### Array Commands

- **Push data to an array (list)**:

  ```javascript
  redis.rpush("list", "value"); // Adds to the end
  redis.lpush("list", "value"); // Adds to the beginning
  ```

- **Pull data from an array (list)**:
  ```javascript
  redis.lrange("list", 0, -1).then((values) => console.log(values)); // Get all values from list
  ```

### Expiry Commands

- **Set an expiry time for a key (in seconds)**:

  ```javascript
  redis.expire("key", 3600); // Key expires in 3600 seconds (1 hour)
  ```

- **Set a key with an expiry time**:
  ```javascript
  redis.set("key", "value", "EX", 3600); // Key expires in 3600 seconds (1 hour)
  ```

### Connect to Redis

To connect to Redis in a Node.js application:

```javascript
const Redis = require("ioredis");
const redis = new Redis(); // Connects to localhost:6379 by default
```

### Disconnect from Redis

To disconnect from Redis:

```javascript
redis.quit();
```

### Connect and Disconnect on Node Server Start/Stop

To connect to Redis when the Node server starts and disconnect when it stops, you can use the following pattern:

```javascript
const Redis = require("ioredis");
let redis;

function startServer() {
  redis = new Redis();
  console.log("Connected to Redis");

  // Your server code here
}

function stopServer() {
  redis.quit().then(() => {
    console.log("Disconnected from Redis");
    // Your server shutdown code here
  });
}

// Start the server
startServer();

// Handle server shutdown
process.on("SIGINT", stopServer);
process.on("SIGTERM", stopServer);
```

This setup ensures that the Redis client is properly connected when the server starts and disconnected when the server stops.

---
