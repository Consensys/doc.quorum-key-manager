---
description: Quorum Key Manager command line interface reference
---

# Quorum Key Manager command line

This reference describes the syntax of the Quorum Key Manager Command Line Interface (CLI) options.

## Options

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

=== "Command Line"

    ```bash
    --http-host=127.0.0.1
    ```

=== "Environment Variable"

    ```bash
    HTTP_HOST="127.0.0.1"
    ```

Host to expose HTTP service.

### `http-port`

=== "Syntax"

    ```bash
    --http-port=<PORT>
    ```

=== "Command Line"

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

=== "Command Line"

    ```bash
    --log-formatter="text"
    ```

=== "Environment Variable"

    ```bash
    LOG_FORMATTER="text"
    ```

Log formatter.
The options are "text" and "json".
The default is "text".

### `log-level`

=== "Syntax"

    ```bash
    --log-level=<STRING>
    ```

=== "Command Line"

    ```bash
    --log-level="debug"
    ```

=== "Environment Variable"

    ```bash
    LOG_LEVEL="debug"
    ```

Log level.
The options are "debug", "error", "fatal", "info", "panic", "trace", and "warn".
The default is "info".

### `log-timestamp`

=== "Syntax"

    ```bash
    --log-timestamp[=<BOOLEAN>]
    ```

=== "Command Line"

    ```bash
    --log-timestamp
    ```

=== "Environment Variable"

    ```bash
    LOG_TIMESTAMP=true
    ```

Enables logging with timestamp (only in "text" format).
The default is `true`.

### `manifest-path`

=== "Syntax"

    ```bash
    --manifest-path=<PATH>
    ```

=== "Command Line"

    ```bash
    --manifest-path=/config/default.yml
    ```

=== "Environment Variable"

    ```bash
    MANIFEST_PATH="/config/default.yml"
    ```

Path to manifest file/folder to configure key manager stores and nodes.
