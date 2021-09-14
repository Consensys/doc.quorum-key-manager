---
description: Building Quorum Key Manager from source code
---

# Build from source

## Prerequisites

- [Go version 1.15 or later](https://golang.org/doc/install)
- C compiler such as [GCC](https://gcc.gnu.org/)
- [Postgres](https://www.postgresql.org/)

## Installation on Linux / Unix / macOS

### Clone the Quorum Key Manager Repository

Clone the `Consensys/quorum-key-manager` repository:

```bash
git clone https://github.com/Consensys/quorum-key-manager.git
```

### Build Quorum Key Manager

After cloning, go to the `quorum-key-manager` directory:

```bash
cd quorum-key-manager
```

Install the project vendors:

```bash
go mod download
```

Compile the binary:

```bash
go build -o ./build/bin/key-manager
```

Display help information and confirm installation:

```bash
./build/bin/key-manager run --help
```

### Create an alias

You can optionally create an alias:

```bash
alias key-manager="<PATH-TO-QUORUM-KEY-MANAGER>/build/bin/key-manager"
```

### Start Quorum Key Manager

Firstly, we need to specify environment variables to connect to Postgres service:
```bash
export DB_HOST=localhost
export DB_PORT=5432
export DB_DATABASE=qkm
```

Run required database migration for Quorum Key Manager service:
```bash
key-manager migrate up [OPTIONS]
```

Start Quorum Key Manager specifying the path to a [manifest file|folder](../HowTo/Use-Manifest-File/Overview.md) and any other [options](../Reference/CLI-Syntax.md):

```bash
key-manager run --manifest-path=<PATH> [OPTIONS]
```
