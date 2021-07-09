---
description: Description of stores
---

# Stores

## Store Manager

Store Manager is the main core component allowing to manage stores.
It is used by other components in the Key-Manager to access a store and perform crypto-operations with it.

A store is a module able to interface with an underlying secure system storage (such as Hashicorp Vault, Azure Key Vault, AWS KMS, etc.) to perform crypto-operations.
Stores implement common interfaces so they can be easily reused (e.g. by the JSON-RPC Proxy).
We define a few store interfaces exposing different crypto-operations which are detailed in  the following Stores section.

Internally the Store Manager holds a map storeName -> Store where storeName is set by a user as part of the store manifest.

The Store Manifest is the object allowing users to specify the configuration for a Store.
Manifest are used by the Store Manager to create Stores  to connect to an underlying secure storage system.
In the first version Store Manifests are yamls on a file system loaded once when starting the Key-Manager.
In the future we could implement more advanced patterns for Store Manifests loading

## Stores

A store is a module able to interface with an underlying secure system storage (such as Hashicorp Vault, Azure Key Vault, AWS KMS, etc.) to perform crypto-operations.

Stores should implement some common interfaces exposing different types of crypto-operations at various levels of abstraction.

In the first implementation we define 3 interfaces of store: Secret Store, Key Store, Ethereum Account Store.
In the future it would perfectly be possible to add other interfaces (e.g ZK Store, Certificate Store, etc.).

### Secret Store

Secret store is a basic store allowing to store and access secret values but does not expose any crypto-operation.

Depending on the implementation a secret store:

- allows to manage multiple versions of a secret
- proposes advanced capabilities to delete and recover secrets

```go
// Store is responsible to store secrets
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

    // GetDeleted secrets
    GetDeleted(ctx context.Context, id string) (*types.Secret, error)

    // ListDeleted secrets
    ListDeleted(ctx context.Context, count uint, skip string) (secrets []*types.Secret, next string, err error)

    // Undelete restore a previously deleted secret not yet permanently deleted
    Undelete(ctx context.Context, id string) error

    // Destroy secret permanently
    Destroy(ctx context.Context, id string, versions ...int) error
}
```

### Key Store

Key store is a store that manages keys allowing it to perform crypto operations such as signature or encryption.

A key store allows to generate or import keys but does not allow access to the private part of the key.

Depending on the implementation a key store:

- allows to manage multiple versions of a key
- proposes advanced capabilities to delete and recover keys

In terms of abstraction it is perfectly possible to have implement a key store:

- connecting to an underlying external dependency and delegating crypto-operations to the external dependency
- using an underlying secret store and performing crypto-operations locally

```go
// KeyStore is responsible to store keys and perform crypto operations
type KeyStore interface {
    store.Store

    // Create a new key and stores it
    Create(ctx context.Context, id string, alg *types.Algo, attr *types.Attributes) (*types.Key, error)

    // Import an externally created key and stores it
    Import(ctx context.Context, id string, privKey []byte, alg *types.Algo, attr *types.Attributes) (*types.Key, error)

    // Get the public part of a stored key.
    Get(ctx context.Context, id string, version int) (*types.Key, error)

    // List keys
    List(ctx context.Context, count uint, skip string) (keys []*types.Key, next string, err error)

    // Update key tags
    Update(ctx context.Context, id string, attr *types.Attributes) (*types.Key, error)

    // Delete secret not permanently, by using Undelete the keysecret can be retrieve
    Delete(ctx context.Context, id string, versions ...int) (*types.Key, error)

    // GetDeleted keys
    GetDeleted(ctx context.Context, id string)

    // ListDeleted keys
    ListDeleted(ctx context.Context, count uint, skip string) (keys []*types.Key, next string, err error)

    // Undelete a previously deleted keysecret
    Undelete(ctx context.Context, id string) error

    // Destroy keysecret permanently
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

When creating a key, the store expects some characteristics about the crypto algorithm for the key.
Those characteristics are attached to the key

```go
type Algo struct {
    // Type of key (e.g. ecdsa, rsa)
    Type string

    // EllipticCurve (e.g secp256k1)
    EllipticCurve string

    // Size of the key
    Size int
}
```

### Ethereum Account Store

Ethereum Account Store is a store that manages Ethereum Accounts allowing to perform Ethereum related crypto-operations.

An account store allows to generate or import accounts but does not allow access to the private key of any key.

In terms of abstraction it is likely that the best approach is to implement an account store based on an underlying key store to perform signature while the account store is responsible to perform Ethereum specific processing/formatting/encoding.

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

### Types

// StoreInfo for a store
type StoreInfo struct {
    // Kind of store
    Kind string

    // Name set by user
    Name string

    // Info about the store proper to each implementation
    // It should not expose any secret information about the store configuration
    Info interface{}

    // Tags set by user when creating the stores
    Tags map[string]string
}

// Metadata are generated by the store attached to stored items
type Metadata struct {
    Version int

    CreatedAt time.Time
    UpdatedAt time.Time
    DeletedAt time.Time
    PurgeAt   time.Time
}

// CryptoOperation type of crypto operation
type CryptoOperation int

// RecoveryPolicy policies for recovering a deleted item
type RecoveryPolicy int

// Attributes are user set configuration and information attached to stored item
type Attributes struct {
    // Operations supported by a stored item (e.g sign, verify, encrypt...)
    Operations []CryptoOperation

    // Enabled wether item is enabled
    Enabled bool

    // ExpireAt expiration date
    ExpireAt time.Time

    // Recovery policy about a key after being deleted before being destroyed
    Recovery struct {
        // Policy for recovery
        Policy RecoveryPolicy

        // Period for recovery
        Period time.Time
    }

    // Tags attached to a stored item
    Tags map[string]string
}

// Secret
type Secret struct {
    // Secret Value
    Value []byte

    // Attributes
    Attr *Attributes

    // Metadata generated by the store
    Metadata *Metadata
}

// Key public part of a key
type Key struct {
    // Secret Value
    PublicKey []byte

    // KeyCryptoAttributes
    Type *KeyType

    // Attr
    Attr *Attributes

    // Metadata generated by the store
    Metadata *Metadata
}

// Type
type KeyType struct {
    // Type of key (e.g. ecdsa, eddsa, rsa)
    Algorithm string

    // EllipticCurve (e.g secp256k1)
    EllipticCurve string

    // Size of the key
    Size int
}

type Account struct {
    Address string

    // Attr
    Attr *Attributes

    // Metadata generated by the store
    Metadata *Metadata
}

### Stores abstraction

// Below a recap of store structs with the interface they should match

type AccountStore struct {
    keyStore keys.Store
    ...
} // matches the account.Store interface


type HashicorpKeyStore struct{...} // matches the keys.Store interface
type AKVKeyStore struct{...}       // matches the keys.Store interface
type AWSKeyStore struct{...}    // matches the keys.Store interface

type KeyStore struct {
    secretStore secrets.Store
    ...
} // matches the keys.Store interface

type HashicorpSecretStore struct{...}  // matches the secrets.Store interface
type AKVSecretStore struct{...}        // matches the secrets.Store interface
type AWSSecretStore struct{...}     // matches the secrets.Store interface
type MemorySecretStore struct{...}     // matches the secrets.Store interface
type FileSystemSecretStore struct{...} // matches the secrets.Store interface
