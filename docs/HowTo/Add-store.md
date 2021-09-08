---
description: Add stores using manifest
---

# Add Store to Quorum Key Manager

There are three kind of stores Quorum Key Manager supports:

- `Secret Store`: It is used to store secrets resources.
- `Key Store`: It is used to store key pairs.
- `Ethereum Store`: It is used to store ethereum wallets.

## Secret Store

Use the following fields to configure one or more Secret store:

- `kind`: *string* - type of secret store (`AKVSecrets`, `AWSSecrets`, `HashicorpSecrets`)
- `version`: *string* - store version
- `name`: *string* - name of the store
- `specs`: *object* - configuration object to connect to an underlying Vault. [See below](#vault-specs)
    !!! note

        If using an `Eth1Account` store, specify any valid `keystore` (`AwsKeys`, `AzureKeys`, or `HashicorpKeys`) under
        `specs`, and provide the `specs` fields for that key store, as shown in the [example](#sample-manifests).

## Key Store

Use the following fields to configure one or more Key store:

- `kind`: *string* - values are: `AKVKeys`, `AWSKeys`, `HashicorpKeys`, `LocalKeys`
- `version`: *string* - store version
- `name`: *string* - name of the store
- `specs`: *object* - configuration object to connect to an underlying Vault. [See below](#vault-specs)
    !!! note

        If using an `LocalKeys` store requires to specify a valid SecretStore (`AWSSecret`, `AKVSecret`, or `HashicorpSecret`) under
        `specs`, and provide the `specs` fields for that key store, as shown in the [example](#sample-manifests).

## Ethereum Store

Use the following fields to configure one or more Ethereum store:

- `kind`: *string* - available values are: `Ethereum`
- `version`: *string* - store version
- `name`: *string* - name of the store
- `specs`: *object* - configuration object to connect to an underlying Vault. [See below](#vault-specs)
    !!! note

        If using an `Eth1Account` store, specify any valid Key Store (`AwsKeys`, `AzureKeys`, or `HashicorpKeys`) under
        `specs`, and provide the `specs` fields for that key store, as shown in the [example](#sample-manifests).


## Vault specs

Depending of the selected Vault service you might need to specify one of the following `spec` in your manifest

### Hashicorp

If using a `HashicorpKeys` or `HashicorpSecrets` kind:
    - `mountPoint`: *string* - secret engine mounting point
    - `address`: *string* - HashiCorp server URL
    - `tokenPath`: *string* - path to token file
    - `token`: *string* - authorization token
    - `namespace`: *string* - default namespace to store data in HashiCorp

!!! note

    `tokenPath` and `token` are mutually exclusive

### Azure Key Vault

If using an `AKVKeys` or `AKVSecrets` kind:
    - `vaultName`: *string* - connected Azure key vault ID
    - `tenantID`: *string* - Azure Active Directory tenant ID
    - `clientID`: *string* - user client ID
    - `clientSecret`: *string* - user client secret

### Amazon Key Management Service

If using an `AWSKeys` or `AWSSecrets` kind:
    - `accessID`: *string* - AWS access ID
    - `secretKey`: *string* - AWS secret key
    - `region`: *string* - AWS region
    - `debug`: *boolean* - indicates whether to enable debugging

## Sample manifests

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
        namespace: user1_space

    # Local key store manifest
    - kind: LocalKeys
      version: 0.0.1
      name: local-keys
      specs:
        secretstore: HashicorpSecrets
        specs:
           mountPoint: secret
           address: http://hashicorp:8200
           tokenPath: path/to/token_file
           namespace: user1_space

    # Eth1 account store manifest
    - kind: Ethereum
      version: 0.0.1
      name: eth1-accounts
      specs:
        keystore: HashicorpKeys
        specs:
          mountPoint: orchestrate
          address: http://hashicorp:8200
          token: YOUR_TOKEN
          namespace: user1_space
    ```
