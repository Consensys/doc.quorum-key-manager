---
description: How to authenticate QKM using TLS.
---

# Authenticate with TLS

You can [authenticate](../../Concepts/Authentication.md#authentication) incoming Quorum Key Manager (QKM) requests using TLS.

Specify a TLS certificate authority (CA) certificate with the [`--auth-tls-ca`](../../Reference/CLI-Syntax.md#auth-tls-ca)
command line option when starting QKM.

!!! example "Starting Quorum Key Manager with TLS authentication"

    ```bash
    key-manager run --auth-tls-ca=ca.crt --manifest-path=/config/default.yml
    ```

The CA certificate must contain one or more CAs to validate client certificates presented to QKM.

If a client presents a valid certificate signed by one of the CAs, then the client is authenticated.

QKM extracts the following user information from the subject field of the client certificate:

- Username and [tenant](../../Concepts/Authorization.md#tenant) from the common name (CN) (for example, `/CN=tenant|user`)
- [Roles](../../Concepts/Authorization.md#role) from the certificate's organization (O) (for example, `/O=role1/O=role2`)
- [Permissions](../../Concepts/Authorization.md#permission) from the certificate's organization unit (OU) (for example, `/OU=*:read/O=secret:write`)

You can use the `openssl` command line tool to generate a certificate signing request:

!!! example "Example certificate signing request"

    ```bash
    openssl req -new -key jbeda.pem -out jbeda-csr.pem -subj "/CN=auth0|alice/O=admin/OU=sign:eth1Account"
    ```
