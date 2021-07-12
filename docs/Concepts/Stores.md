---
description: Description of stores
---

# Stores

## Stores

A store is a Quorum Key Manager (QKM) component that interfaces with an underlying secure system storage (such as HashiCorp
Vault, Azure Key Vault, and AWS KMS) to perform crypto-operations.

You can configure a store using a [store manifest](../HowTo/Use-Manifest-File.md#store-manifest).

The store manager is a QKM component that uses store manifests to create and manage stores.
Other QKM components use the store manager to access stores and perform crypto-operations.

Stores implement common interfaces exposing different types of crypto-operations at different levels of abstraction, so
they can be easily reused (for example, by the JSON-RPC proxy).

QKM defines the following store interfaces:

- Secret store
- Key store
- Ethereum account store

### Secret store

A secret store is a basic store that enables storing and accessing secret values, but does not expose any crypto-operations.

Depending on the implementation, a secret store:

- Can manage multiple versions of a secret.
- Has advanced capabilities to delete and recover secrets.

See [the REST API documentation](https://consensys.github.io/quorum-key-manager/#tag/Secrets) for calls the client can
use to interact with a secret store.

### Key Store

A key store is a store that manages keys and enables crypto-operations such as signing and encryption.

A key store can generate and import keys, but does not allow access to the private part of a key.

Depending on the implementation, a key store:

- Can manage multiple versions of a key.
- Has advanced capabilities to delete and recover keys.

You can implement a key store:

- Connecting and delegating crypto-operations to an external dependency.
- Using an underlying secret store and performing crypto-operations locally.

See [the REST API documentation](https://consensys.github.io/quorum-key-manager/#tag/Keys) for calls the client can use
to interact with a key store.

### Ethereum account store

An Ethereum account store is a store that manages Ethereum accounts and performs Ethereum-related crypto-operations.

An account store can generate and import accounts but does not allow access to the private key of any account.

You can implement an account store based on an underlying key store to perform signing, while the account store is
responsible for performing Ethereum-specific processing/formatting/encoding.

See [the REST API documentation](https://consensys.github.io/quorum-key-manager/#tag/Ethereum-Account) for calls the
client can use to interact with an Ethereum account store.
