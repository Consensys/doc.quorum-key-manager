---
description: How to import resources
---

# Import resources

If you have [Ethereum accounts](../Concepts/Stores.md#ethereum-store), [keys](../Concepts/Stores.md#key-store), or
[secrets](../Concepts/Stores.md#secret-store) in a secure storage system, you can import these resources for use
within Quorum Key Manager (QKM).
Import resources from a store into your local QKM database using the [`import` subcommand](../Reference/CLI/CLI-Subcommands.md#import).

Use `import ethereum` to import Ethereum accounts, `import keys` to import keys, and `import secrets` to import secrets.
You can specify options [on the command line](#on-the-command-line) or [as environment variables](#as-environment-variables).

!!! note

    When you import resources, the private keys remain in the underlying secure storage system.
    The keys are loaded into your local database to generate metadata linked to the underlying system.

## On the command line

Specify the path to the manifest file on which the store is configured using the `--manifest-path` command line option.
Specify the name of the store using the `--import-store-name` option.
Include [any database options](../Reference/CLI/CLI-Syntax.md#db-database) (any options that begin with `--db-`) that
apply to your local database.

!!! example "Importing keys from `hashicorp-keys` on the command line"

    ```bash
    key-manager import keys --manifest-path="/config/default.yml" --import-store-name="hashicorp-keys" --db-database="postgres" --db-host=127.0.0.1 --db-port=6174
    ```

## As environment variables

You can specify the [same options](#on-the-command-line) as environment variables.

!!! example "Importing keys from `hashicorp-keys` as environment variables"

    ```text
    MANIFEST_PATH="/config/default.yml"
    IMPORT_STORE_NAME="hashicorp-keys"
    DB_DATABASE="postgres"
    DB_HOST=127.0.0.1
    DB_PORT=6174
    ```

    ```bash
    key-manager import keys
    ```
