---
description: Quorum Key Manager command line interface reference
---

# Quorum Key Manager command line

This reference describes the syntax of the Quorum Key Manager Command Line Interface (CLI) options.

## Options

You can specify Quorum Key Manager options:

- On the command line.

  ```bash
  key-manager run [OPTIONS]
  ```

- As environment variables.

### `db-database`

=== "Syntax"

    ```bash
    --db-database=<STRING>
    ```

=== "Example"

    ```bash
    --db-database="postgres"
    ```

=== "Environment variable"

    ```bash
    DB_DATABASE="postgres"
    ```

Target database name.
The default is `postgres`.

### `db-host`

=== "Syntax"

    ```bash
    --db-host=<HOST>
    ```

=== "Example"

    ```bash
    --db-host=127.0.0.1
    ```

=== "Environment variable"

    ```bash
    DB_HOST="127.0.0.1"
    ```

Database host.
The default is `127.0.0.1`.

### `db-keepalive`

=== "Syntax"

    ```bash
    --db-keepalive=<DURATION>
    ```

=== "Example"

    ```bash
    --db-keepalive=1m0s
    ```

=== "Environment variable"

    ```bash
    DB_KEEPALIVE="1m0s"
    ```

Number of seconds after which a TCP `keepalive` message should be sent.
The default is `1m0s`.

### `db-password`

=== "Syntax"

    ```bash
    --db-password=<STRING>
    ```

=== "Example"

    ```bash
    --db-password="postgres"
    ```

=== "Environment variable"

    ```bash
    DB_PASSWORD="postgres"
    ```

Database user password.
The default is `postgres`.

### `db-pool-timeout`

=== "Syntax"

    ```bash
    --db-pool-timeout=<DURATION>
    ```

=== "Example"

    ```bash
    --db-pool-timeout=30s
    ```

=== "Environment variable"

    ```bash
    DB_POOL_TIMEOUT="30s"
    ```

Number of seconds for which the client waits for a free connection if all connections are busy.
The default is `30s`.

### `db-poolsize`

=== "Syntax"

    ```bash
    --db-poolsize=<INTEGER>
    ```

=== "Example"

    ```bash
    --db-poolsize=20
    ```

=== "Environment variable"

    ```bash
    DB_POOLSIZE="20"
    ```

Maximum number of connections on the database.

### `db-port`

=== "Syntax"

    ```bash
    --db-port=<PORT>
    ```

=== "Example"

    ```bash
    --db-port=6174
    ```

=== "Environment variable"

    ```bash
    DB_PORT="6174"
    ```

Database port.
The default is `5432`.

### `db-sslmode`

=== "Syntax"

    ```bash
    --db-sslmode=<STRING>
    ```

=== "Example"

    ```bash
    --db-sslmode="require"
    ```

=== "Environment variable"

    ```bash
    DB_PORT="require"
    ```

TLS/SSL mode to connect to database (one of `require`, `disable`, `verify-ca`, and `verify-full`).
The default is `disable`.

### `db-tls-ca`

=== "Syntax"

    ```bash
    --db-tls-ca=<STRING>
    ```

=== "Example"

    ```bash
    --db-tls-ca=tls_ca.pem
    ```

=== "Environment variable"

    ```bash
    DB_TLS_CA="tls_ca.pem"
    ```

Path to TLS certificate authority (CA) in PEM format.

### `db-tls-cert`

=== "Syntax"

    ```bash
    --db-tls-cert=<STRING>
    ```

=== "Example"

    ```bash
    --db-tls-cert=tls_cert.pem
    ```

=== "Environment variable"

    ```bash
    DB_TLS_CERT="tls_cert.pem"
    ```

Path to TLS certificate to connect to database in PEM format.

### `db-tls-key`

=== "Syntax"

    ```bash
    --db-tls-key=<STRING>
    ```

=== "Example"

    ```bash
    --db-tls-key=tls_key.pem
    ```

=== "Environment variable"

    ```bash
    DB_TLS_KEY="tls_key.pem"
    ```

Path to TLS private key to connect to database in PEM format.

### `db-user`

=== "Syntax"

    ```bash
    --db-user=<STRING>
    ```

=== "Example"

    ```bash
    --db-user="postgres"
    ```

=== "Environment variable"

    ```bash
    DB_USER="postgres"
    ```

Database user.
The default is `postgres`.

### `health-port`

=== "Syntax"

    ```bash
    --health-port=<PORT>
    ```

=== "Example"

    ```bash
    --health-port=6174
    ```

=== "Environment variable"

    ```bash
    HEALTH_PORT="6174"
    ```

Port to expose Health HTTP service.
The default is `8081`.

### `help`

=== "Syntax"

    ```bash
    -h, --help, [command] --help
    ```

Print help information and exit, or if a command is specified, print more information about the command.

### `http-host`

=== "Syntax"

    ```bash
    --http-host=<HOST>
    ```

=== "Example"

    ```bash
    --http-host=127.0.0.1
    ```

=== "Environment variable"

    ```bash
    HTTP_HOST="127.0.0.1"
    ```

Host to expose HTTP service.

### `http-port`

=== "Syntax"

    ```bash
    --http-port=<PORT>
    ```

=== "Example"

    ```bash
    --http-port=6174
    ```

=== "Environment variable"

    ```bash
    HTTP_PORT="6174"
    ```

Port to expose HTTP service.
The default is `8080`.

### `log-format`

=== "Syntax"

    ```bash
    --log-format=<STRING>
    ```

=== "Example"

    ```bash
    --log-formatter="text"
    ```

=== "Environment variable"

    ```bash
    LOG_FORMATTER="text"
    ```

Log formatter.
The options are `text` and `json`.
The default is `text`.

### `log-level`

=== "Syntax"

    ```bash
    --log-level=<STRING>
    ```

=== "Example"

    ```bash
    --log-level="debug"
    ```

=== "Environment variable"

    ```bash
    LOG_LEVEL="debug"
    ```

Log level.
The options are `debug`, `error`, `fatal`, `info`, `panic`, `trace`, and `warn`.
The default is `info`.

### `log-timestamp`

=== "Syntax"

    ```bash
    --log-timestamp[=<BOOLEAN>]
    ```

=== "Example"

    ```bash
    --log-timestamp
    ```

=== "Environment variable"

    ```bash
    LOG_TIMESTAMP=true
    ```

Enables logging with timestamp (only in `text` format).
The default is `true`.

### `manifest-path`

=== "Syntax"

    ```bash
    --manifest-path=<PATH>
    ```

=== "Example"

    ```bash
    --manifest-path=/config/default.yml
    ```

=== "Environment variable"

    ```bash
    MANIFEST_PATH="/config/default.yml"
    ```

Path to [manifest file/folder](../HowTo/Use-Manifest-File/Overview.md) to configure key manager stores and nodes.
