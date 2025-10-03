# CALDERA Setup Guide

This guide provides instructions for setting up CALDERA using Docker.

## What is CALDERA?

CALDERA is an automated adversary emulation platform developed by MITRE. It's used for cybersecurity testing and red team operations.

## Prerequisites

- Windows Subsystem for Linux (WSL) installed and configured
- Git installed in WSL
- Docker Desktop for Windows with WSL 2 backend enabled
- Sufficient disk space for the Docker image (recommended: 10GB+)

## Installation Steps

### 0. Verify Docker is Running in WSL

Ensure Docker Desktop is running and WSL integration is enabled:

```bash
docker --version
docker ps
```

If Docker commands don't work, open Docker Desktop settings and enable WSL 2 integration for your Linux distribution.

### 1. Clone the Repository

Clone the CALDERA repository with all submodules:

```bash
git clone https://github.com/mitre/caldera.git --recursive
```

### 2. Navigate to the Directory

Change into the CALDERA directory:

```bash
cd caldera
```

### 3. Build the Docker Image

Build the Docker image with Windows build support:

```bash
docker build --build-arg WIN_BUILD=true . -t caldera:server
```

**Note**: The `WIN_BUILD=true` argument enables Windows agent support. This process may take several minutes.

### 4. Run the Container

Start the CALDERA server with the following port mappings:

```bash
docker run -p 7010:7010 -p 7011:7011/udp -p 7012:7012 -p 8888:8888 caldera:server
```

## Port Mappings

- **7010**: HTTP API and web interface
- **7011/udp**: UDP contact for agents
- **7012**: TCP contact for agents
- **8888**: Main web application interface

## Accessing CALDERA

Once the container is running, access the CALDERA web interface from your Windows browser at:

```
http://localhost:8888
```

**WSL Note**: Since Docker Desktop for Windows forwards ports automatically, you can access the application directly from Windows using `localhost`.

Default credentials (check the logs or documentation for current defaults):
- Username: `admin`
- Password: `admin`

## Troubleshooting

### WSL-Specific Issues

- **Docker not found**: Ensure Docker Desktop is running and WSL integration is enabled in Docker Desktop settings
- **Permission denied**: Run `sudo usermod -aG docker $USER` then restart WSL
- **Slow performance**: Make sure your project files are in the WSL filesystem (e.g., `~/caldera`) not in `/mnt/c/`
- **Port conflicts**: Check if Windows applications are using the required ports

### General Issues

- **Build fails**: Ensure Docker has sufficient resources allocated in Docker Desktop settings
- **Cannot access web interface**: Try `http://127.0.0.1:8888` or check Windows Firewall settings
- **Submodules missing**: Make sure you used the `--recursive` flag when cloning

## Additional Resources

- [Official CALDERA Documentation](https://caldera.readthedocs.io/)
- [CALDERA GitHub Repository](https://github.com/mitre/caldera)

## Security Note

CALDERA is a powerful adversary emulation tool. Only use it in authorized environments for legitimate security testing purposes.