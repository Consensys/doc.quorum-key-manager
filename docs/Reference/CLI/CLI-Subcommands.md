---
description: Quorum Key Manager command line interface subcommands
---

# Quorum Key Manager subcommands

This reference describes the syntax of the Quorum Key Manager (QKM) command line interface (CLI) subcommands.

You can specify QKM subcommands on the command line:

```bash
key-manager [SUBCOMMAND] [SUBCOMMAND OPTIONS]
```

## `import`

[Imports resources](../../HowTo/Import-Resources.md) from a store.

### `ethereum`

=== "Syntax"

    ```bash
    key-manager import ethereum --manifest-path=<PATH> --import-store-name=<STRING> [--db-*]
    ```

=== "Example"

    ```bash
    key-manager import ethereum --manifest-path="/config/default.yml" --import-store-name="eth-accounts" --db-database="postgres" --db-host=127.0.0.1 --db-port=6174
    ```

Imports Ethereum accounts from the specified [Ethereum store](../../Concepts/Stores.md#ethereum-store) configured in the
specified [manifest file](../../HowTo/Use-Manifest-File) into the local QKM database.

You must specify the path of the manifest file using the `--manifest-path` option or the `MANIFEST_PATH` environment variable.

You must specify the name of the store from which import the resources using the `--import-store-name` option or the
`IMPORT_STORE_NAME` environment variable.

You can include any [database options or environment variables](CLI-Syntax.md#db-database) (any options that begin with `--db-`).

### `keys`

=== "Syntax"

    ```bash
    key-manager import keys --manifest-path=<PATH> --import-store-name=<STRING> [--db-*]
    ```

=== "Example"

    ```bash
    key-manager import keys --manifest-path="/config/default.yml" --import-store-name="hashicorp-keys" --db-database="postgres" --db-host=127.0.0.1 --db-port=6174
    ```

Imports keys from the specified [key store](../../Concepts/Stores.md#key-store) configured in the specified
[manifest file](../../HowTo/Use-Manifest-File) into the local QKM database.

You must specify the path of the manifest file using the `--manifest-path` option or the `MANIFEST_PATH` environment variable.

You must specify the name of the store from which import the resources using the `--import-store-name` option or the
`IMPORT_STORE_NAME` environment variable.

You can include any [database options or environment variables](CLI-Syntax.md#db-database) (any options that begin with `--db-`).

### `secrets`

=== "Syntax"

    ```bash
    key-manager import secrets --manifest-path=<PATH> --import-store-name=<STRING> [--db-*]
    ```

=== "Example"

    ```bash
    key-manager import secrets --manifest-path="/config/default.yml" --import-store-name="hashicorp-secrets" --db-database="postgres" --db-host=127.0.0.1 --db-port=6174
    ```

Imports secrets from the specified [secret store](../../Concepts/Stores.md#ethereum-store) configured in the
specified [manifest file](../../HowTo/Use-Manifest-File) into the local QKM database.

You must specify the path of the manifest file using the `--manifest-path` option or the `MANIFEST_PATH` environment variable.

You must specify the name of the store from which import the resources using the `--import-store-name` option or the
`IMPORT_STORE_NAME` environment variable.

You can include any [database options or environment variables](CLI-Syntax.md#db-database) (any options that begin with `--db-`).
