---
title: Quorum Key Manager
description: Quorum Key Manager
---

# Quorum Key Manager

## What is Quorum Key Manager?

Quorum Key Manager is an Ethereum account and key management service developed under the
[BSL 1.1 license] and written in Go. Quorum Key Manager is a signing service that manages accounts
and keys for the entire Quorum stack, and supports the following vaults:

- HashiCorp Vault
- Azure Key Vault
- AWS Key Management Service.

![Architecture](Images/Simplified_Architecture.png)

## Why use Quorum Key Manager?

Manage your user private keys from a single API while having the keys stored in a secure vault.
Manage a user's access rights using authentication and authorization, and audit the access history
and signing requests for registered keys.

Quorum Key Manager is compatible with GoQuorum, Hyperledger Besu, Codefi Orchestrate, and Tessera.

## Quorum Key Manager features

### Security

- Supports JWT or OpenID for authentication.
- Supports role-based access control (RBAC) for authorization.
- Enterprise and cloud-based vault support.

### Versatility

- Supports public and private Ethereum networks.
- Supports multiple cryptographic curves.

<!--links-->
[BSL 1.1 license]: https://mariadb.com/bsl11/
