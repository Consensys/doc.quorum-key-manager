---
description: Description of stores
---

# Stores

A store is a Quorum Key Manager (QKM) component that interfaces with an underlying secure system storage (such as HashiCorp
Vault, Azure Key Vault, or AWS KMS) to perform crypto-operations.

The store manager is a QKM component that uses [store manifest](../HowTo/Use-Manifest-File.md#store-manifest) to create and manage stores.
Other QKM components use the store manager to access stores and perform crypto-operations.

QKM defines the following store interfaces:

- Secret store
- Key store
- Ethereum account store

## Secret store

A secret store allows you to store and access secret values, but doesn't expose any crypto-operations.

Depending on the implementation, a secret store:

- Can manage multiple versions of a secret.
- Has advanced capabilities to delete and recover secrets.

You can use the [`/secrets`](https://consensys.github.io/quorum-key-manager/#tag/Secrets) REST API endpoint to interact with a secret store.

## Key Store

A key store manages keys and enables crypto-operations such as signing and encryption.

A key store can generate and import keys, but doesn't allow access to the private part of a key.

Depending on the implementation, a key store:

- Can manage multiple versions of a key.
- Has advanced capabilities to delete and recover keys.

You can implement a key store to:

- Delegate crypto-operations to an external dependency.
- Use the underlying secret store to perform crypto-operations locally.

You can use the [`/keys`](https://consensys.github.io/quorum-key-manager/#tag/Keys) REST API endpoint to interact with a key store.

## Ethereum account store

An Ethereum account manages Ethereum accounts and performs Ethereum-related crypto-operations (for example, signing transactions).

An account store can generate and import accounts but doesn't allow access to the private key of any account.

You can implement an account store based on an underlying key store to perform signing, while the account store is
responsible for performing Ethereum-specific processing, formatting, and encoding.

You can use the [`/eth1`](https://consensys.github.io/quorum-key-manager/#tag/Ethereum-Account) REST API endpoint to
interact with an Ethereum account store.
