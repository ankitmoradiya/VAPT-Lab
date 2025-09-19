# Prowler Docker Installation

## Prerequisites

- [Docker Compose](https://docs.docker.com/compose/install/) installed

## Installation Steps

1. **Download the required configuration files:**
   ```bash
   curl -LO https://raw.githubusercontent.com/prowler-cloud/prowler/refs/heads/master/docker-compose.yml
   curl -LO https://raw.githubusercontent.com/prowler-cloud/prowler/refs/heads/master/.env
   ```

2. **Start the Prowler App containers:**
   ```bash
   docker compose up -d
   ```

3. **Access the application:**
   
   Open your browser and navigate to [http://localhost:3000](http://localhost:3000)

## Platform Compatibility

Containers are built for `linux/amd64`. If your workstation's architecture is incompatible, use one of these solutions:

- **Set environment variable:**
  ```bash
  export DOCKER_DEFAULT_PLATFORM=linux/amd64
  ```

- **Use platform flag in Docker commands:**
  ```bash
  --platform linux/amd64
  ```

## AWS Role Assumption (Optional)

If you need AWS role assumption functionality, mount your local `.aws` directory:

```bash
# Add this volume mount to your docker-compose.yml or docker run command
- "${HOME}/.aws:/home/prowler/.aws:ro"
```

## Available Docker Images

- **Prowler CLI:** `prowlercloud/prowler`
- **Prowler App:** Available through the docker-compose setup

## Getting Started

After installation, sign up using your email and password at [http://localhost:3000](http://localhost:3000) to begin using Prowler App.