---
description: How to authenticate QKM with OpenID Connect and JWTs.
---

# Authenticate with JSON Web Tokens

You can [authenticate](../../Concepts/Auth.md#authentication) incoming Quorum Key Manager (QKM) requests with the
[OpenID Connect (OIDC)](https://openid.net/connect/) standard using [JSON Web Tokens (JWTs)](https://jwt.io/).
Refer to the [OIDC documentation](https://openid.net/specs/openid-connect-core-1_0.html) for detailed information.

## Runtime options

You can set the following options at QKM runtime to configure OIDC authentication.

- `--auth-oidc-issuer-url`
- `--auth-oidc-ca-file`
- `--auth-oidc-claim-username`
- `--auth-oidc-claim-groups`
- `--auth-oidc-claim-metadata`
