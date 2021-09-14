---
description: Authentication concept page
---

# User authentication

You can configure user authentication with Quorum Key Manager (QKM).
This is optional but recommended.

To authenticate to QKM, users must provide credentials in every request through one of the following methods:

- [OIDC](../HowTo/Authenticate/OIDC.md) - OpenID Connect standard using JSON Web Tokens
- [TLS](../HowTo/Authenticate/TLS.md) - Client TLS authentication
- [API key](../HowTo/Authenticate/API-Key.md) - Set of keys defined in a CSV file and loaded at startup

The authentication process consists of challenging incoming request credentials.
If credentials are valid, QKM extracts user information and attaches it to the request context.
If credentials are invalid, QKM rejects the request.
If no credentials are passed, QKM processes the request as an anonymous request.

After QKM authenticates a request, it submits the request to the targeted service to [authorize](Authorization.md) it.
