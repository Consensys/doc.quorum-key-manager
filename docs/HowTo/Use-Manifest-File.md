---
description: Using a manifest file
---

# Using the Quorum Key Manager manifest file

Use a YAML manifest file to specify Quorum Key Manager manifests.
Manifests represent the configuration of runtime components of the key manager, such as stores and nodes.

Specify the path to the manifest file using the `--manifest-path` option on key manager startup.

## YAML specification

A store manifest contains the following fields to configure a store:

- `kind`: *string* - type of store (for example, AzureKeys or HashicorpSecrets)
- `version`: *string* - store version
- `name`: *string* - name of the store for later reference
- `specs`: *object* - configuration object to connect to an underlying secure system storage
- `tags`: *map* of *strings* to *strings* - (optional) user set information about the store

A node manifest contains the following fields to configure a node:

- `kind`: *string* - "Node"
- `version`: *string* - node version
- `name`: *string* - name of the node for later reference
- `specs`: *object* - configuration object to connect to various endpoints
- `tags`: *map* of *strings* to *strings* - (optional) user set information about the node

You can define multiple manifests in one manifest file, separated by `-`.

!!! example "Sample Quorum Key Manager manifest file"

    ```yaml
    // Hashicorp secret store manifest
    - kind: HashicorpSecrets
      version: 0.0.1
      name: hashicorp-secrets
      specs:
        mountPoint: secret
        address: http://hashicorp:8200
        tokenPath: /vault/token/.root
        namespace: ''

    // Hashicorp key store manifest
    - kind: HashicorpKeys
      version: 0.0.1
      name: hashicorp-keys
      specs:
        mountPoint: orchestrate
        address: http://hashicorp:8200
        tokenPath: /vault/token/.root
        namespace: ''

    // GoQuorum node manifest
    - kind: Node
      version: 0.0.0
      name: goquorum-node
      specs:
        rpc:
          addr: http://goquorum1:8545
        tessera:
          addr: http://tessera1:9080

    // Besu node manifest
    - kind: Node
      version: 0.0.0
      name: besu-node
      specs:
        rpc:
          addr: http://validator1:8545
    ```

!!! example "Starting Quorum Key Manager with a manifest file"

    ```bash
    quorum-kms run --manifest-path=/config/manifest.yml
    ```
