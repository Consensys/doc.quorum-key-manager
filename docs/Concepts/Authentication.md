---
description: Authentication concept page
---

# Authentication

Quorum Key Manager (QKM) authentication is inspired by the Kubernetes authentication mechanism.

QKM does not internally store or represent user objects.
Instead, it attaches user information to every incoming request.

The authentication process consists of challenging incoming request authentication credentials, and if credentials are valid,
extracting user information and attaching it to the request context.
If no credentials are passed, the request is not rejected and processed as an anonymous request.

If not rejected during the authentication process, the request is submitted to the targeted service which is responsible
for performing [authorization](Authorization.md) checks based on request context before performing service operations.

To successfully authenticate to QKM, users (or clients) are expected to present some credentials into every request.
Credentials can be passed through three methods of authentication:

- [OIDC](../HowTo/Authenticate/JWT.md) - OpenID Connect standard using JSON Web Tokens
- [TLS](../HowTo/Authenticate/TLS.md) - Client TLS authentication
- [API key](../HowTo/Authenticate/API-Key.md) - Set of keys defined in a CSV file and loaded at startup
