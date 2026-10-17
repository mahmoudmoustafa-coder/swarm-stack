# Docker Swarm Stack - Nginx

## Overview

This project deploys an Nginx web server using Docker Swarm Stack.

It demonstrates service replication, port publishing, health checks, and basic container monitoring.

## Project Architecture

- **Orchestrator:** Docker Swarm
- **Web Server:** Nginx
- **Replicas:** 3
- **Host Port:** 8082
- **Container Port:** 80
- **Health Checks:** Enabled
- **Restart Policy:** On failure

## Prerequisites

- Ubuntu Linux
- Docker Engine
- Docker Swarm initialized on the manager node

## Project Structure

```text
swarm-stack/
├── compose.yaml
├── .gitignore
└── README.md
```

## Deployment

Deploy the stack using the Compose file:

```bash
docker stack deploy -c compose.yaml webstack
```

## Verify the Deployment

### Check Stack Services

```bash
docker stack services webstack
```

### Check Service Tasks

```bash
docker service ps webstack_web
```

### Check Running Containers and Health

```bash
docker ps --filter name=webstack_web
```

### Test the Web Server

```bash
curl -I http://localhost:8082
```

A successful HTTP response indicates that Nginx is responding to requests.

## Configuration

The `compose.yaml` file defines:

- Three replicas of the Nginx service.
- Port publishing from host port `8082` to container port `80`.
- A health check that requests the local Nginx homepage.
- A health-check interval of 40 seconds.
- A health-check timeout of 5 seconds.
- Three retries before marking a container unhealthy.
- A health-check start period of 10 seconds.
- A restart policy that applies when a task fails.

## Scaling the Service

To change the number of replicas, update `deploy.replicas` in `compose.yaml`.

For example:

```yaml
deploy:
  replicas: 3
```

Apply the configuration:

```bash
docker stack deploy -c compose.yaml webstack
```

Verify the updated replica count:

```bash
docker stack services webstack
```

## Monitoring and Troubleshooting

### Monitor Container Resource Usage

```bash
docker stats
```

### View Service Logs

```bash
docker service logs --tail 20 webstack_web
```

### Inspect Service Tasks

```bash
docker service ps webstack_web
```

### Check Container Health

```bash
docker ps --filter name=webstack_web
```

Containers should show `healthy` when their configured health checks succeed.

## Remove the Stack

Remove the stack and its managed services:

```bash
docker stack rm webstack
```

## Learning Outcomes

- Deploying applications using Docker Swarm.
- Managing replicated services.
- Publishing application ports.
- Configuring container health checks.
- Inspecting service tasks and container status.
- Monitoring resource usage and application logs.
- Updating stack configurations.

## Author

Mahmoud Moustafa
