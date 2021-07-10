---
description: Description of stores
---

# Stores

## Stores

A store is a Quorum Key Manager (QKM) component that interfaces with an underlying secure system storage (such as HashiCorp
Vault, Azure Key Vault, and AWS KMS) to perform crypto-operations.

You can configure a store using a [store manifest](../HowTo/Use-Manifest-File.md#store-manifest).

The store manager is a main QKM component that uses store manifests to create and manage stores.
Other QKM components use the store manager to access stores and perform crypto-operations.

Stores implement common interfaces exposing different types of crypto-operations at different levels of abstraction, so
they can be easily reused (for example, by the JSON-RPC proxy).

Quorum Key Manager defines the following store interfaces:

- Secret store
- Key store
- Ethereum account store

### Secret store

A secret store is a basic store that enables storing and accessing secret values, but does not expose any crypto-operations.

Depending on the implementation, a secret store:

- Can manage multiple versions of a secret.
- Has advanced capabilities to delete and recover secrets.

Secret store specification:

```go
type Store interface {
    store.Store

    // Set secret
    Set(ctx context.Context, id string, value []byte, attr *types.Attributes) (*types.Metadata, error)

    // Get a secret
    Get(ctx context.Context, id string, version int) (*types.Secret, error)

    // List secrets
    List(ctx context.Context, count uint, skip string) (secrets []*types.Secret, next string, err error)

    // Update secret attributes
    Update(ctx context.Context, id string, attr *types.Attributes)

    // Delete secret not permanently, by using Undelete the secret can be restored
    Delete(ctx context.Context, id string, versions ...int) (*types.Secret, error)

    // Get deleted secrets
    GetDeleted(ctx context.Context, id string) (*types.Secret, error)

    // List deleted secrets
    ListDeleted(ctx context.Context, count uint, skip string) (secrets []*types.Secret, next string, err error)

    // Restore a previously deleted secret not yet permanently deleted
    Undelete(ctx context.Context, id string) error

    // Destroy a secret permanently
    Destroy(ctx context.Context, id string, versions ...int) error
}
```

### Key Store

A key store is a store that manages keys and enables crypto-operations such as signing and encryption.

A key store can generate and import keys, but does not allow access to the private part of a key.

Depending on the implementation, a key store:

- Can manage multiple versions of a key.
- Has advanced capabilities to delete and recover keys.

You can implement a key store:

- Connecting and delegating crypto-operations to an external dependency.
- Using an underlying secret store and performing crypto-operations locally.

Key store specification:

```go
type KeyStore interface {
    store.Store

    // Create a new key and store it
    Create(ctx context.Context, id string, alg *types.Algo, attr *types.Attributes) (*types.Key, error)

    // Import an externally created key and store it
    Import(ctx context.Context, id string, privKey []byte, alg *types.Algo, attr *types.Attributes) (*types.Key, error)

    // Get the public part of a stored key
    Get(ctx context.Context, id string, version int) (*types.Key, error)

    // List keys
    List(ctx context.Context, count uint, skip string) (keys []*types.Key, next string, err error)

    // Update key tags
    Update(ctx context.Context, id string, attr *types.Attributes) (*types.Key, error)

    // Delete Key not permanently, by using undelete the key can be retrieved
    Delete(ctx context.Context, id string, versions ...int) (*types.Key, error)

    // Get deleted keys
    GetDeleted(ctx context.Context, id string)

    // List deleted keys
    ListDeleted(ctx context.Context, count uint, skip string) (keys []*types.Key, next string, err error)

    // Restore a previously deleted key not permanently deleted
    Undelete(ctx context.Context, id string) error

    // Destroy a key permanently
    Destroy(ctx context.Context, id string, versions ...int) error

    // Sign from a digest using the specified key
    Sign(ctx context.Context, id string, data []byte) ([]byte, error)

    // Verify a signature using a specified key
    Verify(ctx context.Context, id string, data []byte) (*types.Metadata, error)

    // Encrypt an arbitrary sequence of bytes using an encryption key that is stored in a key vault
    Encrypt(ctx context.Context, id string, data []byte) ([]byte, error)

    // Decrypt a single block of encrypted data.
    Decrypt(ctx context.Context, id string, data []byte) (*types.Metadata, error)
}
```

### Ethereum account store

An Ethereum account store is a store that manages Ethereum accounts and performs Ethereum-related crypto-operations.

An account store can generate and import accounts but does not allow access to the private key of any account.

You can implement an account store based on an underlying key store to perform signing, while the account store is
responsible for performing Ethereum-specific processing/formatting/encoding.

Ethereum account store specification:

```go
type ETHStore interface {
    store.Store

    // Create an account
    Create(ctx context.Context, attr *types.Attributes) (*types.Account, error)

    // Import an externally created key and store account
    Import(ctx context.Context, privKey []byte, attr *types.Attributes) (*types.Account, error)

    // Get account
    Get(ctx context.Context, addr string) (*types.Account, error)

    // List accounts
    List(ctx context.Context, count uint, skip string) (accounts []*types.Account, next string, err error)

    // Update account attributes
    Update(ctx context.Context, addr string, attr *types.Attributes) (*types.Account, error)

    // Delete account not permanently, by using Undelete the account can be retrieve
    Delete(ctx context.Context, addrs ...string) (*types.Account, error)

    // GetDeleted accounts
    GetDeleted(ctx context.Context, addr string)

    // ListDeleted accounts
    ListDeleted(ctx context.Context, count uint, skip string) (keys []*types.Account, next string, err error)

    // Undelete a previously deleted account
    Undelete(ctx context.Context, addr string) error

    // Destroy account permanently
    Destroy(ctx context.Context, addrs ...string) error

    // Sign from a digest using the specified account
    Sign(ctx context.Context, addr string, data []byte) (sig []byte, err error)

    // SignHomestead transaction
    SignHomestead(ctx context.Context, addr string, tx *ethereum.Transaction) (sig []byte, err error)

    // SignEIP155 transaction
    SignEIP155(ctx context.Context, addr string, chainID string, tx *ethereum.Transaction) (sig []byte, err error)

    // SignEEA transaction
    SignEEA(ctx context.Context, addr string, chainID string, tx *ethereum.Transaction, args *ethereum.EEAPrivateArgs) (sig []byte, err error)

    // SignPrivate transaction
    SignPrivate(ctx context.Context, addr string, tx *ethereum.Transaction) (sig []byte, err error)

    // Verify a signature using a specified key
    ECRevocer(ctx context.Context, addr string, data []byte, sig []byte) (*types.Account, error)
}
```
