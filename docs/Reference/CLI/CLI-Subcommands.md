---
description: Quorum Key Manager command line interface subcommands
---

# Quorum Key Manager subcommands

This reference describes the syntax of the Quorum Key Manager command line interface (CLI) subcommands.

You can specify Quorum Key Manager subcommands on the command line:

```bash
key-manager [SUBCOMMAND] [SUBCOMMAND OPTIONS]
```

## `import`

Imports [Ethereum accounts](../../Concepts/Stores.md#ethereum-store), [keys](../../Concepts/Stores.md#key-store), or
[secrets](../../Concepts/Stores.md#secret-store) from the specified [manifest file](../../HowTo/Use-Manifest-File) into
the specified store.

You must specify the path of the manifest file using the `--manifest-path` option or the `MANIFEST_PATH` environment variable.

You must specify the name of the store in which to import the resources using the `--import-store-name` option or the
`IMPORT_STORE_NAME` environment variable.

You can include any [database options or environment variables](CLI-Syntax.md#db-database) (any options that begin with `--db-`).

=== "Syntax"

    ```bash
    key-manager import <ethereum|keys|secrets> --manifest-path=<PATH> --import-store-name=<STRING> [--db-*]
    ```

=== "Ethereum accounts example"

    ```bash
    key-manager import ethereum --manifest-path="/config/default.yml" --import-store-name=<STRING> --db-database="postgres" --db-host=127.0.0.1 --db-port=6174
    ```

=== "Keys example"

    ```bash
    key-manager import keys --manifest-path="/config/default.yml" --import-store-name=<STRING> --db-database="postgres" --db-host=127.0.0.1 --db-port=6174
    ```

=== "Secrets example"

    ```bash
    key-manager import secrets --manifest-path="/config/default.yml" --import-store-name=<STRING> --db-database="postgres" --db-host=127.0.0.1 --db-port=6174
    ```
