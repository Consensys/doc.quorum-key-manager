---
description: Quorum Key Manager command line interface reference
---

# Quorum Key Manager command line options

This reference describes the syntax of the Quorum Key Manager (QKM) command line interface (CLI) options.

## Options

You can specify QKM options:

- On the command line.

    ```bash
    key-manager run [OPTIONS]
    ```

- As environment variables.

### `auth-api-key-file`

=== "Syntax"

    ```bash
    --auth-api-key-file=<FILE>
    ```

=== "Example"

    ```bash
    --auth-api-key-file=api_key_file.csv
    ```

=== "Environment variable"

    ```bash
    AUTH_API_KEY_FILE="api_key_file.csv"
    ```

When using [API key authentication](../../HowTo/Authenticate/API-Key.md), path to the API key CSV file.

### `auth-oidc-issuer-url`

=== "Syntax"

    ```bash
    --auth-oidc-issuer-url=<URL>
    ```

=== "Example"

    ```bash
    --auth-oidc-issuer-url="https://quorum-key-manager.eu.auth0.com/.well-known/jwks.json"
    ```

=== "Environment variable"

    ```bash
    AUTH_OIDC_ISSUER-URL="https://quorum-key-manager.eu.auth0.com/.well-known/jwks.json"
    ```

When using [OAuth 2.0 authentication](../../HowTo/Authenticate/OAuth2.md), URL of the OpenID Connect server.
You must use this option with [`--auth-oidc-ca-cert`](#auth-oidc-ca-cert).

### `auth-oidc-audience`

=== "Syntax"

    ```bash
    --auth-oidc-audience=<AUDIENCE>
    ```

=== "Example"

    ```bash
    --auth-oidc-audience=https://quorum-key-manager.eu.auth0.com
    ```

=== "Environment variable"

    ```bash
    AUTH_OIDC_AUDIENCE="https://quorum-key-manager.eu.auth0.com"
    ```

When using [OAuth 2.0 authentication](../../HowTo/Authenticate/OAuth2.md), expected audience (`aud` field) of access tokens.
You must use this option with [`--auth-oidc-issuer-url`](#auth-oidc-issuer-url).

### `auth-tls-ca`

=== "Syntax"

    ```bash
    --auth-tls-ca=<FILE>
    ```

=== "Example"

    ```bash
    --auth-tls-ca=ca.crt
    ```

=== "Environment variable"

    ```bash
    AUTH_TLS_CA="ca.crt"
    ```

When using [TLS authentication](../../HowTo/Authenticate/TLS.md), path to the certificate authority (CA) certificate for
the TLS server.

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

Number of seconds before the client sends a TCP `keepalive` message.
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

Number of seconds the client waits for a free connection if all connections are busy.
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
    DB_SSLMODE="require"
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

### `https-enable`

=== "Syntax"

    ```bash
    --https-enable
    ```

=== "Example"

    ```bash
    --https-enable
    ```

=== "Environment variable"

    ```bash
    HTTPS_ENABLE=true
    ```

Enable HTTPS server.
This is required when using [TLS authentication](../../HowTo/Authenticate/TLS.md).

### `https-server-cert`

=== "Syntax"

    ```bash
    --https-server-cert=<STRING>
    ```

=== "Example"

    ```bash
    --https-server-cert=tls.crt
    ```

=== "Environment variable"

    ```bash
    HTTPS_SERVER_CERT="tls.crt"
    ```

Path to TLS server certificate.
This is required when using [TLS authentication](../../HowTo/Authenticate/TLS.md).

### `https-server-key`

=== "Syntax"

    ```bash
    --https-server-key=<STRING>
    ```

=== "Example"

    ```bash
    --https-server-key=tls.key
    ```

=== "Environment variable"

    ```bash
    HTTPS_SERVER_KEY="tls.key"
    ```

Path to TLS server key.
This is required when using [TLS authentication](../../HowTo/Authenticate/TLS.md).

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

Path to [manifest file/folder](../../HowTo/Use-Manifest-File/Overview.md) to configure key manager stores and nodes.
