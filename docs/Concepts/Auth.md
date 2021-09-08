---
description: Authentication concept page
---

# Quorum Key Manager authentication and authorization

## Terminology

### Action

### Resource

### Tenant

### Permission

### Role

## Authentication

Quorum Key Manager (QKM) authentication is inspired by the Kubernetes authentication mechanism.

QKM doesn't internally store or represent user objects.
Instead, it attaches user information to every incoming request.

The authentication process consists of challenging incoming request authentication credentials, and if credentials are valid,
extracting user information and attaching it to the request context.
If credentials are invalid, the request is rejected.
If no credentials are passed, the request is processed as an anonymous request.

If not rejected during the authentication process, the request is submitted to the targeted service which is responsible
for performing [authorization](#authorization) checks based on request context before performing service operations.

To authenticate to QKM, users must provide credentials in every request through one of the following methods:

- [OIDC](../HowTo/Authenticate/JWT.md) - OpenID Connect standard using JSON Web Tokens
- [TLS](../HowTo/Authenticate/TLS.md) - Client TLS authentication
- [API key](../HowTo/Authenticate/API-Key.md) - Set of keys defined in a CSV file and loaded at startup

## Authorization

After a request gets through the [authentication](#authentication) process, it's submitted to a Service.
A Service is responsible to proceed to Authorization checks.
If a Service calls another Service both are responsible to perform their own Authorization checks.

When a Service receives a request, two cases can appear:

- The request was authenticated and it holds user information.
- The request was neither authenticated nor rejected and it holds default username `system:anonymous` and group `system:unauthenticated`.

A Service uses Policies to control whether the request is authorized or not to perform a certain Action over the Service.

Policies are attributed to groups, so it's possible to determine which Policies apply to a request by basing on the groups in the User Information.

### Role-based access control

Role-based access control (RBAC) restricts system access to authorized users.

See the [full list of RBAC permissions](../Reference/RBAC-Permissions.md).

### Resource-based access control

Resource-based access control restricts access resource by resource.
