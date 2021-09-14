---
description: Run Quorum Key Manager from Docker image
---

# Run Quorum Key Manager from Docker Compose

A Docker image is provided to run Quorum Key Manager in a Docker container.

## Prerequisites

- [Docker](https://docs.docker.com/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)
- MacOS or Linux

    !!! Important

        The Docker image does not run on Windows.

## Download latest Docker compose

To run Quorum Key Manager download its latest [Docker compose file](https://github.com/ConsenSys/quorum-key-manager/blob/main/docker-compose.latest.yml)

## Setup Quorum Key Manager

Define your setting for Quorum Key Manager service using [manifest files](../HowTo/Use-Manifest-File/Overview.md) and any other [options](../Reference/CLI-Syntax.md):


## Launch Quorum Key Manager

Specify where your manifests can are stored in your filesystem

```bash
export HOST_MANIFEST_PATH={your_manifests_file_or_folder}
```

Start Quorum Key Manager service using docker-compose with the following command:

```bash
docker-compose -f docker-compose.latest.yml up key-manager
```
