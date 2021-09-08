---
description: Role-based access control permissions
---

# Role-based access control permissions

The following tables list the permissions for [role-based access control](../Concepts/Auth.md#role-based-access-control).
Each permission has a list of allowed [REST endpoints](Rest.md).

## Eth1 accounts

| Name                 | Description                                  | Allowed endpoints                    |
| :------------------: | :------------------------------------------: | :----------------------------------: |
| `read:ethAccount`    | Allows reading operations over Eth1 accounts | Get, list, get deleted, list deleted |
| `create:ethAccount`  | Allows creating Eth1 accounts                | Create, import, update               |
| `delete:ethAccount`  | Allows soft-deleting Eth1 accounts           | Delete, restore                      |
| `destroy:ethAccount` | Allows permanently deleting Eth1 accounts    | Delete, restore, destroy             |
| `sign:ethAccount`    | Allows signing and verifying signatures      | *All sign endpoints*, EC recover     |
| `encrypt:ethAccount` | Allows encryption and decryption             | Encrypt, decrypt                     |

## Keys

| Name          | Description                             | Allowed endpoints                    |
| :-----------: | :-------------------------------------: | :----------------------------------: |
| `read:key`    | Allows reading operations over keys     | Get, list, get deleted, list deleted |
| `create:key`  | Allows creating keys                    | Create, import, update               |
| `delete:key`  | Allows soft-deleting keys               | Delete, restore                      |
| `destroy:key` | Allows permanently deleting keys        | Delete, restore, destroy             |
| `sign:key`    | Allows signing and verifying signatures | Sign                                 |
| `encrypt:key` | Allows encryption and decryption        | Encrypt, decrypt                     |

## Nodes

| Name          | Description                          | Allowed endpoints                    |
| :-----------: | :----------------------------------: | :----------------------------------: |
| `read:nodes`  | Allows reading operations over nodes | Get, list, get deleted, list deleted |
| `proxy:nodes` | Allows creating nodes                | Create, update                       |

## Secrets

| Name             | Description                            | Allowed endpoints                    |
| :--------------: | :------------------------------------: | :----------------------------------: |
| `read:secret`    | Allows reading operations over secrets | Get, list, get deleted, list deleted |
| `set:secret`     | Allows creating secrets                | Set, update                          |
| `delete:secret`  | Allows soft-deleting secrets           | Delete, restore                      |
| `destroy:secret` | Allows permanently deleting secrets    | Delete, restore, destroy             |