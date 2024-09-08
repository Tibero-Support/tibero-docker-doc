# Tibero Docker

## Table of Contents
1. [Introduction](#introduction)
2. [License](#license)
3. [Prerequisites](#prerequisites)
4. [Getting Started](#getting-started)
    - [For AMD64](#for-amd64)
    - [For ARM64](#for-arm64)
5. [Verifying the Installation](#verifying-the-installation)

## Introduction

This Docker image provides a ready-to-use Tibero7 database environment. It is built with the demo version of [Tibero database](https://www.tibero.com/).

## License

The license for this image follows the original Tibero demo version license. The terms are as follows:

1. This demo version is for testing and evaluation purposes only.
2. It can be used only for a limited time period, specifically for the duration of the issued license. The image is usable only within the validity period of the license you obtain.
3. It is not permitted for use in production environments.

**To use this image, you must first obtain a license. Please visit the [following link](https://technet.tmax.co.kr/ko/front/main/main.do) to acquire the necessary license**

## Prerequisites

- Docker installed on your system
    - [what is docker](https://docs.docker.com/guides/docker-overview/)
    - [docker tutorial](https://docker-curriculum.com/)

- Basic understanding of Docker commands
    - [docker-compose cheat sheet](https://devhints.io/docker-compose)

## Getting Started

There are 3 ways to get started with this Tibero7 demo Docker image:
* Using Docker Compose
* Running manually with Docker CLI

### For AMD64

#### Option 1: Using Docker Compose

1. Create a `docker-compose.yml` file with the following content:

```yaml
services:
  tibero7:
    container_name: <your-container-name>
    image: ghcr.io/tibero-support/tibero7
    ports:
      - "<host-port>:8629"
    hostname: <license-hostname>
    volumes:
      - <path-to-your-license>:/tibero7/license/license.xml
```

2. Replace the placeholders:
    - `<your-container-name>`: Choose a name for your container
    - `<host-port>`: The port on your host machine to map to Tibero's `8629` port
    - `<license-hostname>`: The hostname you specified when obtaining your Tibero license
    - `<path-to-your-license>`: The path to your Tibero license file on your host machine


3. Run the following command in the directory containing your docker-compose.yml:


    `docker-compose up -d`

#### Option 2: Running Manually with Docker CLI

Use the following command:

For Windows (PowerShell):
```powershell
docker run -d `
  --name <your-container-name> `
  -p <host-port>:8629 `
  -h <license-hostname> `
  -v <path-to-your-license>:/tibero7/license/license.xml `
  ghcr.io/tibero-support/tibero7
```

### For ARM64 Systems

**Note: Tibero currently only provides AMD64 (x86_64) binaries. When running on ARM architectures, you must use emulation.**

**Prerequisites for ARM64**:

- For Docker Desktop on macOS: Enable "Use Rosetta for x86/amd64 emulation on Apple Silicon" in settings.
- For Linux ARM systems: Ensure QEMU is installed and configured for x86_64 emulation.

**Warning**: Running x86_64 binaries on ARM through emulation may impact performance. Consider using native AMD64 hardware for production environments.

#### Option 1: Using Docker Compose

1. Create a `docker-compose.yml` file with the following content:

```yaml
services:
  tibero7:
    container_name: <your-container-name>
    platform: linux/amd64
    image: ghcr.io/tibero-support/tibero7
    ports:
      - "<host-port>:8629"
    hostname: <license-hostname>
    volumes:
      - <path-to-your-license>:/tibero7/license/license.xml
```

2. Replace the placeholders as described in the AMD64 section.


3. Run the following command:


    docker-compose up -d


#### Option 2: Running Manually with Docker CLI

Use the following command:

Replace the placeholders as described earlier.
```bash
docker run -d \
  --name <your-container-name> \
  --platform linux/amd64 \
  -p <host-port>:8629 \
  -h <license-hostname> \
  -v <path-to-your-license>:/tibero7/license/license.xml \
  ghcr.io/tibero-support/tibero7
```

## Verifying the Installation

To check if the container is running:

```bash
docker ps
```
To view the container logs:
```bash
docker logs <your-container-name>
```