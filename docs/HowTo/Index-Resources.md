---
description: How to index resources
---

# Index resources

If you have existing [Ethereum accounts](../Concepts/Stores.md#ethereum-store), [keys](../Concepts/Stores.md#key-store),
or [secrets](../Concepts/Stores.md#secret-store) in a secure storage system, you must index (reference) these resources in
your local QKM database using the [`sync` subcommand](../Reference/CLI/CLI-Subcommands.md#sync) in order to use them.

Use `sync ethereum` to index Ethereum accounts, `sync keys` to index keys, and `sync secrets` to index secrets.
You can specify options [on the command line](#on-the-command-line) or [as environment variables](#as-environment-variables).

!!! important

    When you index your resources, the private keys remain in the underlying secure storage system.
    The keys are loaded into your local database to generate metadata linked to the underlying system.

## On the command line

Specify the path to the manifest file in which the store is configured using the `--manifest-path` command line option,
and the name of the store using the `--store-name` option.
Include [any database options](../Reference/CLI/CLI-Syntax.md#db-database) (any options that begin with `--db-`) that
apply to your local database.

!!! example "Indexing keys from `hashicorp-keys` on the command line"

    ```bash
    key-manager sync keys --manifest-path="/config/default.yml" --store-name="hashicorp-keys" --db-port=8080
    ```

## As environment variables

You can specify the [same options](#on-the-command-line) as environment variables. Using:

- Manifest file by using the [`--manifest-path`](../Reference/CLI/CLI-Syntax.md#manifest-path)
- Database connection settings, such as [`--db-database`](../Reference/CLI/CLI-Syntax.md#db-database)
- Environment variable `SYNC_STORE_NAME` with the identifier of the store to index

!!! example "Indexing keys from `hashicorp-keys` as environment variables"

    ```text
        MANIFEST_PATH="/config/default.yml"
        SYNC_STORE_NAME="hashicorp-keys"
    ```

    ```bash
    key-manager sync keys
    ```
