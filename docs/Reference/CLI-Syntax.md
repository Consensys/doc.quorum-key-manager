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

When using [API key authentication](../HowTo/Authenticate/API-Key.md), path to the API key CSV file.

### `auth-oidc-ca-cert`

=== "Syntax"

    ```bash
    --auth-oidc-ca-cert=<FILE>
    ```

=== "Example"

    ```bash
    --auth-oidc-ca-cert=ca.key
    ```

=== "Environment variable"

    ```bash
    AUTH_OIDC_CA_CERT="ca.key"

When using [OpenID Connect authentication](../HowTo/Authenticate/JWT.md), path to the certificate authority (CA) key for
the OpenID server.
You must use this option with [--auth-oidc-issuer-url](#auth-oidc-issuer-url).

### `auth-oidc-claim-permissions`

=== "Syntax"

    ```bash
    --auth-oidc-claim-permissions=<STRING>
    ```

=== "Example"

    ```bash
    --auth-oidc-claim-permissions="scope"
    ```

=== "Environment variable"

    ```bash
    AUTH_OIDC_CLAIM_PERMISSIONS="scope"

When using [OpenID Connect authentication](../HowTo/Authenticate/JWT.md), claim from which to extract [permissions](RBAC-Permissions.md).
The default is the standard scope `scope`.

### `auth-oidc-claim-roles`

=== "Syntax"

    ```bash
    --auth-oidc-claim-roles=<STRING>
    ```

=== "Example"

    ```bash
    --auth-oidc-claim-roles="qkm.roles"
    ```

=== "Environment variable"

    ```bash
    AUTH_OIDC_CLAIM_ROLES="qkm.roles"

When using [OpenID Connect authentication](../HowTo/Authenticate/JWT.md), claim from which to extract roles.
The default is `qkm.roles`.

### `auth-oidc-claim-username`

=== "Syntax"

    ```bash
    --auth-oidc-claim-username=<STRING>
    ```

=== "Example"

    ```bash
    --auth-oidc-claim-username="sub"
    ```

=== "Environment variable"

    ```bash
    AUTH_OIDC_CLAIM_USERNAME="sub"

When using [OpenID Connect authentication](../HowTo/Authenticate/JWT.md), claim from which to extract the username.
The default is the standard claim `sub`.

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

When using [OpenID Connect authentication](../HowTo/Authenticate/JWT.md), URL of the OpenID Connect server.
You must use this option with [--auth-oidc-ca-cert](#auth-oidc-ca-cert).

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

When using [TLS authentication](../HowTo/Authenticate/TLS.md), path to the certificate authority (CA) certificate for
the TLS server.

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
The default is 8081.

### `help`

=== "Syntax"

    ```bash
    -h, --help
    ```

Print help information and exit.

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

=== "Environment Variable"

    ```bash
    HTTP_PORT="6174"
    ```

Port to expose HTTP service.
The default is 8080.

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
