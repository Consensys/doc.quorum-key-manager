---
description: Run Quorum Key Manager from Docker image
---

# Run Quorum Key Manager from Docker image

A Docker image is provided to run Quorum Key Manager in a Docker container.

## Prerequisites

- [Docker](https://docs.docker.com/install/)
- MacOS or Linux

    !!! Important

        The Docker image does not run on Windows.

## Run Docker image

Run Quorum Key Manager on Docker with the following command:

```bash
docker run -it --name quorum-key-manager -v type=bind,source="$(pwd)"/deps/config,target=/manifests docker.consensys.net/pub/quorum-key-manager:latest run --manifest-path=/manifests
```
