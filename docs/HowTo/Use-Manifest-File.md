---
description: Using a manifest file
---

# Using the Quorum Key Manager manifest file

Use a YAML manifest file to specify the Quorum Key Manager runtime components, such as [stores](../Concepts/Stores.md), [nodes](../Concepts/Nodes.md) and [roles]([stores](../Concepts/Roles.md)).

Specify the path to the manifest file or a path with several files using the [`--manifest-path`](../Reference/CLI-Syntax.md#manifest-path) option on key manager startup, alternately using environment variable `MANIFEST_PATH`

## YAML specification

Use the following fields to configure one or more:

- `kind`: *string* - type of component
- `version`: *string* - store version
- `name`: *string* - name of the store
- `specs`: *object* - configuration object to component

See next the different types of components you can setup using manifest files:
- [store](./Add-store.md)
- [node](./Add-node.md)
- [role](./Define-role.md)


### Node manifest

Use the following fields to configure one or more [nodes](../Concepts/Nodes.md):

- `kind`: *string* - the string `Node`
- `version`: *string* - node version
- `name`: *string* - name of the node
- `specs`: *object* - configuration object to connect to various endpoints, with the following fields for each endpoint:
    - `rpc` or `tessera`: (field name is the name of the endpoint)
        - `addr`: *string* - address of the endpoint
- `tags`: *map* of *strings* to *strings* - (optional) user set information about the node

### Sample loading manifest file

!!! example "Starting Quorum Key Manager with a manifest file"

    ```bash
    key-manager run --manifest-path=/config/manifest.yml
    ```



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
