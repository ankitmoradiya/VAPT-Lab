# MITRE Caldera Docker Installation

## Prerequisites

- Docker installed and running

## Installation Options

### Option 1: Local Build (Recommended)

1. **Clone the repository:**
   ```bash
   git clone https://github.com/mitre/caldera.git --recursive
   cd caldera
   ```

2. **Build the Docker image:**
   ```bash
   docker build --build-arg VARIANT=full -t caldera .
   ```

3. **Run the container:**
   ```bash
   docker run -it -p 8888:8888 caldera
   ```

### Option 2: Pre-Built Image

**Run directly from GitHub Container Registry:**
```bash
docker run -p 8888:8888 ghcr.io/mitre/caldera:latest
```

> **Note:** This container may be slightly outdated. Building locally is recommended.

## Access the Application

Open your browser and navigate to [http://localhost:8888](http://localhost:8888)

**Default credentials:** `red/admin`

## Container Variants

- **full**: Includes all files for `emu` and `atomic` plugins (suitable for offline environments)
- **slim**: Downloads plugin files on-demand (requires internet connection)

To build slim variant:
```bash
docker build --build-arg VARIANT=slim -t caldera-slim .
```

## Port Configuration

Adjust port forwarding as needed for different contacts:
```bash
# Example with custom port
docker run -it -p 8080:8888 caldera
```

## Container Management

**Stop the container gracefully:**
```bash
# Find container ID
docker ps

# Stop container
docker stop <container_ID>
```

## Persistent Data (Optional)

**Mount configuration file:**
```bash
docker run -it -p 8888:8888 -v <your_path>/conf.yml:/usr/src/app/conf/local.yml caldera
```

**Mount data directory:**
```bash
docker run -it -p 8888:8888 -v <path_to_data>:/usr/src/app/data/ caldera
```

## Plugin Data Mounting (Optional)

**For Atomic Red Team plugin:**
```bash
-v <atomic_repo_path>:/usr/src/app/plugins/atomic/data/atomic-red-team
```

**For EMU plugin:**
```bash
-v <emu_repo_path>:/usr/src/app/plugins/emu/data/adversary-emulation-plans
```

## Important Notes

- Container automatically generates keys/usernames/passwords on first start
- Data is ephemeral by default unless volumes are mounted
- The `builder` plugin will not work within Docker
- Ensure proper directory structure when mounting data volumes