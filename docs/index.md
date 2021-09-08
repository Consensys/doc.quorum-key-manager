---
title: Quorum Key Manager
description: Quorum Key Manager
---

# Quorum Key Manager

## What is Quorum Key Manager?

Quorum Key Manager is an Ethereum account and key management service developed under the [BSL 1.1 license] and written in Go.
Quorum Key Manager is a signing service that manages accounts, keys, and secrets for the entire Quorum stack, and supports the
following vaults:

- HashiCorp Vault
- Azure Key Vault
- AWS Key Management Service

![Architecture](Images/Simplified_Architecture.png)

## Why use Quorum Key Manager?

Manage users' secrets, keys and ethereum wallets from a single API while having everything stored in a secure vault, or V3 keystores.

Manage users' access rights using authentication and authorization customizable access policies, and audit every access to your private resources.

Quorum Key Manager is compatible with GoQuorum, Hyperledger Besu, Tessera, and Codefi Orchestrate.

## Quorum Key Manager features

### Security

- Supports TLS, API-Key, OpenID Connect, and other types of authentication.
- Supports role-based access control (RBAC).
- Supports enterprise and cloud-based vaults.

### Versatility

- Supports public and private Ethereum networks.
- Supports every kind of signing transactions, including private transaction
- Support for signing [ethereum message] and [typed data].
- Supports different ecliptic curves, such as eccda and eddsa, and signing algorithm, such as bn254 and secp256k1.
- Supports secrets versioning.

<!--links-->
[BSL 1.1 license]: https://mariadb.com/bsl11/
[typed data]: https://eips.ethereum.org/EIPS/eip-712
[ethereum message]: https://eips.ethereum.org/EIPS/eip-191
