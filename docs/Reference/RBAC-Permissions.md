---
description: Role-based access control permissions
---

# Role-based access control permissions

The following tables list the permissions for [role-based access control](../Concepts/Auth.md#role-based-access-control).

## Secrets

| Name             | Description                            | Allowed endpoints                    |
| :--------------: | :------------------------------------: | :----------------------------------: |
| `read:secret`    | Allows reading operations over secrets | get, list, list deleted, get deleted |
| `set:secret`     | Allows creating secrets                | set, update                          |
| `delete:secret`  | Allows soft-deleting secrets           | delete, undelete                     |
| `destroy:secret` | Allows permanently deleting secrets    | delete, undelete, destroy            |

## Keys

| Name          | Description                             | Allowed endpoints                    |
| :-----------: | :-------------------------------------: | :----------------------------------: |
| `read:key`    | Allows reading operations over keys     | get, list, list deleted, get deleted |
| `create:key`  | Allows creating keys                    | create, import, update               |
| `delete:key`  | Allows soft-deleting keys               | delete, undelete                     |
| `destroy:key` | Allows permanently deleting keys        | delete, undelete, destroy            |
| `sign:key`    | Allows signing and verifying signatures | sign                                 |
| `encrypt:key` | Allows encryption and decryption        | encrypt, decrypt                     |

## Eth1

| Name           | Description                                  | Allowed endpoints                    |
| :------------: | :------------------------------------------: | :----------------------------------: |
| `read:eth1`    | Allows reading operations over eth1 accounts | get, list, list deleted, get deleted |
| `create:eth1`  | Allows creating eth1 accounts                | create, import, update               |
| `delete:eth1`  | Allows soft-deleting eth1 accounts           | delete, undelete                     |
| `destroy:eth1` | Allows permanently deleting eth1 accounts    | delete, undelete, destroy            |
| `sign:eth1`    | Allows signing and verifying signatures      | sign, sign transaction, sign EEA, sign quorum private, sign, sign typed data, EC recover |
| `encrypt:eth1` | Allows encryption and decryption             | encrypt, decrypt                     |

## Stores

| Name            | Description                                | Allowed endpoints                    |
| :-------------: | :----------------------------------------: | :----------------------------------: |
| `read:store`    | Allows reading operations over stores      | get, list, list deleted, get deleted |
| `create:store`  | Allows creating stores                     | create, update                       |
| `delete:store`  | Allows soft-deleting stores                | delete, undelete                     |
| `destroy:store` | Allows permanently deleting stores         | delete, undelete, destroy            |
| `admin:store`   | Allows accessing every resource of a store | *all endpoints*                      |

# Nodes

| Name            | Description                                           | Allowed endpoints                              |
| :-------------: | :---------------------------------------------------: | :--------------------------------------------: |
| `read:nodes`    | Allows reading operations over nodes                  | get, list, list deleted, get deleted           |
| `create:nodes`  | Allows creating nodes                                 | create, update                                 |
| `delete:nodes`  | Allows soft-deleting nodes                            | delete, undelete                               |
| `destroy:nodes` | Allows permanently deleting nodes                     | delete, undelete, destroy                      |
| `proxy:nodes`   | Allows using calls to the underlying blockchain nodes | `eth_send_transaction`, `eea_send_transaction` |
