---
description: How to authenticate QKM with OpenID Connect and JWTs.
---

# Authenticate with JSON Web Tokens

You can [authenticate](../../Concepts/Authentication.md#authentication) incoming Quorum Key Manager (QKM) requests with the
[OpenID Connect (OIDC)](https://openid.net/connect/) standard using [JSON Web Tokens (JWTs)](https://jwt.io/).

User requests can present a JWT through the HTTP `Authorization` header with value `Bearer <token>`.

Refer to the [OIDC documentation](https://openid.net/specs/openid-connect-core-1_0.html) for detailed information.

## Command line options

You can set the following options at QKM runtime to configure OIDC authentication.

- [`--auth-oidc-issuer-url`](../../Reference/CLI-Syntax.md#auth-oidc-issuer-url) - URL of the OpenID Connect server.
- [`--auth-oidc-ca-cert`](../../Reference/CLI-Syntax.md#auth-oidc-ca-cert) - Path to the certificate authority (CA) key for the OpenID server.
- [`--auth-oidc-claim-username`](../../Reference/CLI-Syntax.md#auth-oidc-claim-username) - Claim from which to extract the username.
- [`--auth-oidc-claim-permissions`](../../Reference/CLI-Syntax.md#auth-oidc-claim-permissions) - Claim from which to extract permissions.
- [`--auth-oidc-claim-roles`](../../Reference/CLI-Syntax.md#auth-oidc-claim-roles) - Claim from which to extract roles.

!!! example "Starting Quorum Key Manager with OIDC authentication"

    ```bash
    key-manager run --auth-oidc-issuer-url="https://quorum-key-manager.eu.auth0.com/.well-known/jwks.json" --auth-oidc-ca-cert=ca.key --manifest-path=/config/default.yml
    ```
