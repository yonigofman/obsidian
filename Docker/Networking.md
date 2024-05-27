### Overview

Docker networking is a fundamental aspect of using Docker, allowing containers to communicate with each other and with external networks. This tutorial will cover the basics of Docker networking, including types of networks, creating and managing networks, and connecting containers to networks.

### Table of Contents

1. Introduction to Docker Networking
2. Docker Network Types
3. Creating Docker Networks
4. Connecting Containers to Networks
5. Inspecting Docker Networks
6. Advanced Networking Concepts

### 1. Introduction to Docker Networking

Docker networking enables communication between Docker containers and between containers and external systems. Docker provides several network drivers for different use cases.

### 2. Docker Network Types

Docker supports several types of networks, each suited for different scenarios:

| Network Type | Description |
|--------------|-------------|
| **bridge**   | The default network driver. Suitable for standalone containers and provides basic network isolation. |
| **host**     | Removes network isolation between the Docker host and the container. The container shares the host's networking namespace. |
| **overlay**  | Used for multi-host networking. Enables swarm services to communicate with each other. |
| **macvlan**  | Assigns a MAC address to each container, making it appear as a physical device on the network. |
| **none**     | Disables networking for the container. |

### 3. Creating Docker Networks

You can create a Docker network using the `docker network create` command. Below are examples of creating different types of networks.

#### Bridge Network

```sh
docker network create my-bridge-network
```

#### Overlay Network

```sh
docker network create --driver overlay my-overlay-network
```

#### Macvlan Network

```sh
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  -o parent=eth0 my-macvlan-network
```

### 4. Connecting Containers to Networks

Containers can be connected to networks at creation or later using the `docker network connect` command.

#### Connecting at Creation

```sh
docker run -d --name my-container --network my-bridge-network nginx
```

#### Connecting to an Existing Container

```sh
docker network connect my-bridge-network my-container
```

### 5. Inspecting Docker Networks

You can inspect networks to get detailed information using the `docker network inspect` command.

```sh
docker network inspect my-bridge-network
```

This command provides details such as network configuration, connected containers, and IP address assignments.

### 6. Advanced Networking Concepts

#### Network Aliases

Network aliases allow you to assign additional names to a container's IP address within a network, which can be useful for service discovery.

```sh
docker run -d --name my-container --network my-bridge-network --network-alias my-service nginx
```

#### Custom DNS

You can specify custom DNS servers for a container using the `--dns` option.

```sh
docker run -d --name my-container --network my-bridge-network --dns 8.8.8.8 nginx
```

### Summary

Docker networking is a powerful feature that allows you to control how containers communicate with each other and with external systems. By understanding the different types of networks and how to create and manage them, you can design robust and flexible containerized applications.

### Example Tables

#### Common Docker Network Commands

| Command                              | Description                             |
|--------------------------------------|-----------------------------------------|
| `docker network ls`                  | List all networks                       |
| `docker network create <name>`       | Create a new network                    |
| `docker network inspect <name>`      | Inspect a network                       |
| `docker network connect <name> <container>` | Connect a container to a network |
| `docker network disconnect <name> <container>` | Disconnect a container from a network |
| `docker network rm <name>`           | Remove a network                        |

#### Network Drivers Comparison

| Driver   | Isolated | Supports Multi-Host | Suitable Use Case                     |
|----------|----------|---------------------|---------------------------------------|
| bridge   | Yes      | No                  | Standalone containers                 |
| host     | No       | No                  | High-performance networking            |
| overlay  | Yes      | Yes                 | Swarm services, multi-host communication |
| macvlan  | Yes      | No                  | Network isolation, physical network appearance |
| none     | Yes      | No                  | Disable networking for a container     |
