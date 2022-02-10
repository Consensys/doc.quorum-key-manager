---
description: Add Roles using manifest
---

# Add a role to Quorum Key Manager

You can define a [role](../../Concepts/Authorization.md#role) in a Quorum Key Manager (QKM) [manifest file](Overview.md).

Use the following fields to configure one or more roles:

- `kind`: *string* - the string `Role`
- `name`: *string* - name of the role
- `specs`: *object* - configuration object containing a list of [permissions](../../Reference/RBAC-Permissions.md)
  assigned to the role.

!!! example "Example role manifest file"

    ```yaml
    # Anonymous role manifest (specifies permissions for anonymous requests)
    - kind: Role
      name: anonymous
      specs:
        permissions:
          - "read:nodes"

    # Guest role manifest
    - kind: Role
      name: guest
      specs:
        permissions:
          - "read:*"

    # Signer role manifest
    - kind: Role
      name: signer
      specs:
        permissions:
          - "read:*"
          - "sign:keys"
          - "sign:ethereum"

    # Admin role manifest
    - kind: Role
      name: admin
      specs:
        permissions:
          - "*:*"
    ```
