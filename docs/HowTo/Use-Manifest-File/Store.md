---
description: Add stores using manifest
---

# Add a store to Quorum Key Manager

You can define a [store](../../Concepts/Stores.md) in a Quorum Key Manager (QKM) [manifest file](Overview.md).

QKM supports the following store interfaces:

- [Vault](#vault)
- [Secret store](#secret-store)
- [Key store](#key-store)
- [Ethereum store](#ethereum-store)

!!! important

    If you have existing Ethereum accounts, keys, or secrets in a secure storage system, you must
    [index](../Index-Resources.md) them in your local QKM database in order to use them.

## Vault

Use the following fields to configure one or more [vaults](../../Concepts/Stores.md#vault):

- `kind`: *string* - vgault
- `type`: *string* - supported vault types are `hashicorp`, `azure`, and `aws`
- `name`: *string* - identifier of the vault
- `allowed_tenants`: *array* of *strings* - (optional) list of allowed tenants for this store when using
  [resource-based access control](../../Concepts/Authorization.md#resource-based-access-control)
- `specs`: *object* - [configuration object to connect to an underlying vault](#vault-configuration).

!!! Example "Example vault store manifest file"

    ```yaml
    # Hashicorp secret store manifest
    - kind: Vault
      name: hashicorp-vault
      specs:
        mount_point: secret
        address: http://hashicorp:8200
        token: YOUR_TOKEN
        namespace: user1_space
    ```

If using one of the following vault services, include the corresponding `spec` fields in your manifest.

### HashiCorp

If using a `HashicorpKeys` or `HashicorpSecrets` store:

- `mount_point`: *string* - secret engine mounting point
- `address`: *string* - HashiCorp server URL
- `token_path`: *string* - path to token file
- `token`: *string* - authorization token
- `namespace`: *string* - default namespace to store data in HashiCorp

!!! note

    - `tokenPath` and `token` are mutually exclusive.
    - If using a `Hashicorp` to store keys, you must install the [HashiCorp Vault Plugin](https://github.com/ConsenSys/quorum-hashicorp-vault-plugin).

### Azure Key Vault

If using an `AKVKeys` or `AKVSecrets` store:

- `vault_name`: *string* - connected Azure Key Vault ID
- `tenant_id`: *string* - Azure Active Directory tenant ID
- `client_id`: *string* - user client ID
- `client_secret`: *string* - user client secret

### Amazon Key Management Service

If using an `AWSKeys` or `AWSSecrets` store:

- `access_id`: *string* - AWS access ID
- `secret_key`: *string* - AWS secret key
- `region`: *string* - AWS region
- `debug`: *boolean* - indicates whether to enable debugging

## Secret store

Use the following fields to configure one or more [secret stores](../../Concepts/Stores.md#secret-store):

- `kind`: *string* - Store
- `type`: *string* - secret
- `name`: *string* - name of the secret store
- `allowed_tenants`: *array* of *strings* - (optional) list of allowed tenants for this store when using
  [resource-based access control](../../Concepts/Authorization.md#resource-based-access-control)
- `specs`: *object* - [configuration object to selected injected vault](#vault-configuration).

!!! Example "Example secret store manifest file"

    ```yaml
    # Hashicorp secret store manifest
    - kind: Store
      type: secret
      name: my-secret-store
      specs:
        vault: hashicorp-vault
    ```

## Key store

Use the following fields to configure one or more [key stores](../../Concepts/Stores.md#key-store):

- `kind`: *string* - Store
- `type`: *string* - key
- `name`: *string* - name of the key store
- `allowed_tenants`: *array* of *strings* - (optional) list of allowed tenants for this store when using
  [resource-based access control](../../Concepts/Authorization.md#resource-based-access-control)
- `specs`: *object* - [configuration object to selected vault or secret store](#vault-configuration).

!!! Example "Example key store manifest file"

    ```yaml
    # Hashicorp key store manifest
    - kind: Store
      type: key
      name: my-key-store
      specs:
        vault: hashicorp-vault

    # Local key store manifest
    - kind: Store
      type: local-keys
      name: my-key-store
      specs:
        secret_store: my-secret-store
    ```

## Ethereum store

Use the following fields to configure one or more [Ethereum stores](../../Concepts/Stores.md#ethereum-store):

- `kind`: *string* - Store
- `type`: *string* - Ethereum
- `name`: *string* - name of the Ethereum store
- `allowed_tenants`: *array* of *strings* - (optional) list of allowed tenants for this store when using
  [resource-based access control](../../Concepts/Authorization.md#resource-based-access-control)
- `specs`: *object* - [configuration object to selected key store](#vault-configuration).

!!! Example "Example Ethereum store manifest file"

    ```yaml
    # Ethereum store manifest
    - kind: Store
      type: ethereum
      name: my-ethereum-store
      specs:
        key_store: hashicorp-keys
    ```
