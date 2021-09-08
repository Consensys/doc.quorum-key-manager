---
description: Authentication concept page
---

# Quorum Key Manager authentication and authorization

## Authentication

To authenticate to Quorum Key Manager (QKM), users must provide credentials in every request through one of the following methods:

- [OIDC](../HowTo/Authenticate/JWT.md) - OpenID Connect standard using JSON Web Tokens
- [TLS](../HowTo/Authenticate/TLS.md) - Client TLS authentication
- [API key](../HowTo/Authenticate/API-Key.md) - Set of keys defined in a CSV file and loaded at startup

The authentication process consists of challenging incoming request authentication credentials.
If credentials are valid, QKM extracts user information and attaches it to the request context.
If credentials are invalid, QKM rejects the request.
If no credentials are passed, QKM processes the request as an anonymous request.

## Authorization

After QKM [authenticates](#authentication) a request, it submits the request to the targeted service which performs
authorization checks based on request context before performing service operations.

The authorization process restricts system access through [role-based access control (RBAC)](#role-based-access-control)
or [resource-based access control](#resource-based-access-control).

### Terminology

- **Action** - A functionality of your application to restrict to some users.
  For example, read, create, sign, encrypt, delete, and destroy.
- **Resource** - A representation of a business entity, to be managed by your application.
  Authorization restricts access over resources.
  QKM currently has the following resources:

    | Name         | Description                                                         |
    | :----------: | :-----------------------------------------------------------------: |
    | Alias        | A representation of an external public key. For example, a [Tessera](https://docs.tessera.consensys.net/en/stable/) address. |
    | Eth1 account | A cryptographic key allowing interaction with the Ethereum network. |
    | Key          | A cryptographic key.                                                |
    | Node         | A representation of an underlying blockchain node.                  |
    | Secret       | A key-value element stored in a secure vault system.                |
    | Store        | A set of secrets, keys, or Eth1 accounts.                           |

- **Tenant** - The highest access level to resources.
  In [resource-based access control](#resource-based-access-control), you must pass a list of allowed tenants when defining a
  resource [manifest file](../HowTo/Use-Manifest-File.md).
- **Permission** - An authorization of an action over a resource, used in [role-based access control (RBAC)](#role-based-access-control).
  An identity provider assigns [permissions](../Reference/RBAC-Permissions.md) to users, and your application receives
  them at each request.
  Permissions take the form `action:resource` and are not mutually exclusive.
- **Role** - A named set of permissions defined by a [manifest](../HowTo/Use-Manifest-File.md).
  Alternatively, you can [use Auth0 to specify roles](https://auth0.com/docs/authorization/rbac/roles/create-roles) and
  attach permissions to your token.

### Role-based access control

Role-based access control (RBAC) restricts actions over resources to authorized users.

See the [full list of RBAC permissions](../Reference/RBAC-Permissions.md).

### Resource-based access control

Resource-based access control restricts access resource by resource.
