---
description: Using a manifest file
---

# Using the Quorum Key Manager manifest file

Use a YAML manifest file to specify Quorum Key Manager manifests.
Manifests represent the configuration of runtime components of the key manager, such as stores and nodes.

Specify the path to the manifest file using the [`--manifest-path`](../Reference/CLI-Syntax.md#manifest-path) option on key manager startup.

## YAML specification

### Store manifest

A store manifest contains the following fields to configure a store:

- `kind`: *string* - type of store (`AwsKeys`, `AwsSecrets`, `AzureKeys`, `AzureSecrets`, `Eth1Account`, `HashicorpKeys`,
  or `HashicorpSecrets`)
- `version`: *string* - store version
- `name`: *string* - name of the store for later reference
- `specs`: *object* - configuration object to connect to an underlying secure system storage, with the following fields:
    - If using an `AwsKeys` or `AwsSecrets` store:
        - `accessID`: *string* - AWS access ID
        - `secretKey`: *string* - AWS secret key
        - `region`: *string* - AWS region
        - `debug`: *boolean* - indicates whether to enable debugging
    - If using an `AzureKeys` or `AzureSecrets` store:
        - `vaultName`: *string* - connected AKV key vault ID
        - `tenantID`: *string* - Azure Active Directory tenant ID
        - `clientID`: *string* - user client ID
        - `clientSecret`: *string* - user client secret
    - If using a `HashicorpKeys` or `HashicorpSecrets` store:
        - `mountPoint`: *string* - secret engine mounting point
        - `address`: *string* - HashiCorp server URL
        - `tokenPath`: *string* - path to token file
        - `token`: *string* - authorization token
        - `namespace`: *string* - default namespace to store data in HashiCorp

    !!! note

        If using an `Eth1Account` store, specify any valid `keystore` (`AwsKeys`, `AzureKeys`, or `HashicorpKeys`) under
        `specs`, and provide the `specs` fields for that key store, as shown in the [example](#sample-manifest-file).

- `tags`: *map* of *strings* to *strings* - (optional) user set information about the store

### Node manifest

A node manifest contains the following fields to configure a node:

- `kind`: *string* - the string `Node`
- `version`: *string* - node version
- `name`: *string* - name of the node for later reference
- `specs`: *object* - configuration object to connect to various endpoints, with the following fields for each endpoint:
    - `rpc` or `tessera`: (field name is the name of the endpoint)
        - `addr`: *string* - address of the endpoint
- `tags`: *map* of *strings* to *strings* - (optional) user set information about the node

### Sample manifest file

You can define multiple manifests in one manifest file, each separated by a dash (`-`).

The following example shows a manifest file containing secret store, key store, Eth1 account store, and node manifests.

!!! example "Sample Quorum Key Manager manifest file"

    ```yaml
    # Hashicorp secret store manifest
    - kind: HashicorpSecrets
      version: 0.0.1
      name: hashicorp-secrets
      specs:
        mountPoint: secret
        address: http://hashicorp:8200
        tokenPath: path/to/token_file
        token: YOUR_TOKEN
        namespace: user1_space

    # Hashicorp key store manifest
    - kind: HashicorpKeys
      version: 0.0.1
      name: hashicorp-keys
      specs:
        mountPoint: orchestrate
        address: http://hashicorp:8200
        tokenPath: path/to/token_file
        token: YOUR_TOKEN
        namespace: user1_space

    # Eth1 account store manifest
    - kind: Eth1Account
      version: 0.0.1
      name: eth1-accounts
      specs:
        keystore: HashicorpKeys
        specs:
          mountPoint: orchestrate
          address: http://hashicorp:8200
          token: YOUR_TOKEN
          namespace: user1_space

    # GoQuorum node manifest
    - kind: Node
      version: 0.0.0
      name: goquorum-node
      specs:
        rpc:
          addr: http://goquorum1:8545
        tessera:
          addr: http://tessera1:9080

    # Besu node manifest
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
