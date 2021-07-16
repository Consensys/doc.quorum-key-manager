---
description: Building Quorum Key Manager from source code
---

# Build from source

## Prerequisites

- [Go version 1.15 or later](https://golang.org/doc/install)
- C compiler such as [GCC](https://gcc.gnu.org/)

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
make gobuild
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

Start Quorum Key Manager specifying the path to a [manifest file](../HowTo/Use-Manifest-File.md) and any other [options](../Reference/CLI-Syntax.md):

```bash
key-manager run --manifest-path=<PATH> [OPTIONS]
```
