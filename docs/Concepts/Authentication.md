---
description: Authentication concept page
---

# Authentication

To authenticate to Quorum Key Manager (QKM), users must provide credentials in every request through one of the following methods:

- [OIDC](../HowTo/Authenticate/JWT.md) - OpenID Connect standard using JSON Web Tokens
- [TLS](../HowTo/Authenticate/TLS.md) - Client TLS authentication
- [API key](../HowTo/Authenticate/API-Key.md) - Set of keys defined in a CSV file and loaded at startup

The authentication process consists of challenging incoming request authentication credentials.
If credentials are valid, QKM extracts user information and attaches it to the request context.
If credentials are invalid, QKM rejects the request.
If no credentials are passed, QKM processes the request as an anonymous request.

After QKM authenticates a request, it submits the request to the targeted service which performs
[authorization](Authorization.md) checks based on request context before performing service operations.
