---
description: Using a manifest file
---

# Using the Quorum Key Manager manifest file

Use a YAML manifest file to configure the Quorum Key Manager (QKM) runtime components.
You can configure:

- [Stores](Store.md).
- [Nodes](Node.md).
- [Roles](Role.md).

You can define multiple manifests in one manifest file, each separated by a dash (`-`).

!!! example "Example Quorum Key Manager manifest file"

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

Specify the path to the manifest file or to a directory with several manifest files using the [`--manifest-path`](../../Reference/CLI-Syntax.md#manifest-path)
command line option on QKM startup. You can alternatively use the `MANIFEST_PATH` environment variable.

!!! example "Starting Quorum Key Manager with a manifest file"

    ```bash
    key-manager run --manifest-path=/config/manifest.yml
    ```
