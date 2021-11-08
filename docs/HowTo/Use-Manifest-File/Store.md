---
description: Add stores using manifest
---

# Add a store to Quorum Key Manager

You can define a [store](../../Concepts/Stores.md) in a Quorum Key Manager (QKM) [manifest file](Overview.md).

QKM supports the following store interfaces:

- [Secret store](#secret-store)
- [Key store](#key-store)
- [Ethereum store](#ethereum-store)

!!! important

    If you have existing Ethereum accounts, keys, or secrets in a secure storage system, you must
    [index](../Index-Resources.md) them in your local QKM database in order to use them.

## Secret store

Use the following fields to configure one or more [secret stores](../../Concepts/Stores.md#secret-store):

- `kind`: *string* - type of secret store (`AKVSecrets`, `AWSSecrets`, `HashicorpSecrets`)
- `version`: *string* - store version
- `name`: *string* - name of the store
- `alowedTenants`: *array* of *strings* - (optional) list of allowed tenants for this store when using
  [resource-based access control](../../Concepts/Authorization.md#resource-based-access-control)
- `specs`: *object* - [configuration object to connect to an underlying vault](#vault-configuration).

!!! Example "Example secret store manifest file"

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
    ```

## Key store

Use the following fields to configure one or more [key stores](../../Concepts/Stores.md#key-store):

- `kind`: *string* - type of key store (`AKVKeys`, `AWSKeys`, `HashicorpKeys`, `LocalKeys`)
- `version`: *string* - store version
- `name`: *string* - name of the store
- `alowedTenants`: *array* of *strings* - (optional) list of allowed tenants for this store when using
  [resource-based access control](../../Concepts/Authorization.md#resource-based-access-control)
- `specs`: *object* - [configuration object to connect to an underlying vault](#vault-configuration).

!!! note

    - If using a `HashicorpKeys` store, you must install the [HashiCorp Vault Plugin](https://github.com/ConsenSys/quorum-hashicorp-vault-plugin).
    - If using a `LocalKeys` store, specify any valid `secretstore` (`AWSSecret`, `AKVSecret`, or `HashicorpSecret`) under
      `specs`, and provide the `specs` fields for that secret store, as shown in the following example.

!!! Example "Example key store manifest file"

    ```yaml
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
    ```

## Ethereum store

Use the following fields to configure one or more [Ethereum stores](../../Concepts/Stores.md#ethereum-store):

- `kind`: *string* - the string `Ethereum`
- `version`: *string* - store version
- `name`: *string* - name of the store
- `alowedTenants`: *array* of *strings* - (optional) list of allowed tenants for this store when using
  [resource-based access control](../../Concepts/Authorization.md#resource-based-access-control)
- `specs`: *object* - configuration object containing any valid `keystore` (`AKVKeys`, `AWSKeys`, `HashicorpKeys`, `LocalKeys`),
  and the `specs` fields for that key store, as shown in the following example

!!! Example "Example Ethereum store manifest file"

    ```yaml
    # Ethereum store manifest
    - kind: Ethereum
      version: 0.0.1
      name: eth-accounts
      specs:
        keystore: HashicorpKeys
        specs:
          mountPoint: orchestrate
          address: http://hashicorp:8200
          token: YOUR_TOKEN
          namespace: user1_space
    ```

## Vault configuration

If using one of the following vault services, include the corresponding `spec` fields in your manifest.

### HashiCorp

If using a `HashicorpKeys` or `HashicorpSecrets` store:

- `mountPoint`: *string* - secret engine mounting point
- `address`: *string* - HashiCorp server URL
- `tokenPath`: *string* - path to token file
- `token`: *string* - authorization token
- `namespace`: *string* - default namespace to store data in HashiCorp

!!! note

    `tokenPath` and `token` are mutually exclusive.

### Azure Key Vault

If using an `AKVKeys` or `AKVSecrets` store:

- `vaultName`: *string* - connected Azure Key Vault ID
- `tenantID`: *string* - Azure Active Directory tenant ID
- `clientID`: *string* - user client ID
- `clientSecret`: *string* - user client secret

### Amazon Key Management Service

If using an `AWSKeys` or `AWSSecrets` store:

- `accessID`: *string* - AWS access ID
- `secretKey`: *string* - AWS secret key
- `region`: *string* - AWS region
- `debug`: *boolean* - indicates whether to enable debugging
