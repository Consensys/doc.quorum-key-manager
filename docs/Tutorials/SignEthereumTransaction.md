---
description: Signing an Ethereum transaction tutorial
---

# Sign an Ethereum transaction

This tutorial walks you through signing an Ethereum transaction using Quorum Key Manager.

## Prerequisites

- Quorum Key Manager installed
- [`curl` command line](https://curl.se/download.html)
- A [HashiCorp Vault](https://www.hashicorp.com/products/vault) configured

## Steps

1. In the Quorum Key Manager [manifest file], specify an `Eth1Account` store to allocate your HashiCorp keys.
   Use the following template, filling in the `specs` for `HashicorpKeys` with [information about your HashiCorp Vault]:

    ```yaml
    kind: Eth1Account
    version: 0.0.1
    name: eth1-accounts
    specs:
      keystore: HashicorpKeys
      specs:
        mountPoint: <STORAGE-MOUNTING-POINT>
        address: <SERVER-URL>
        token: <MY-API-TOKEN>
        namespace: <SELECTED-NAMESPACE>
    ```

2. Run Quorum Key Manager with the manifest file loaded, using the [`--manifest-path`](../Reference/CLI-Syntax.md#manifest-path) option:

    ```bash
    quorum-kms run --manifest-path=<PATH-TO-MANIFEST-FILE>
    ```

3. Create an Ethereum account:

    === "curl HTTP request"

        ```bash
        curl -X POST 'quorum-key-manager/stores/eth1-accounts/eth1' --header 'Content-Type: application/json' --data-raw '{"keyId": "test-account", "tags": {"propose": "my-first-example"}}'
        ```

    === "JSON result"

        ```json
        {
            "publicKey": "0x0450fcc403101d428906b1e1dd597551cd8ec51fde32c3383ce5a5f8f288eac0c01652aaf370a0d0813d75c903c5ee3d52a0761177a96800b5b9f780dc64b6a922",
            "compressedPublicKey": "0x0250fcc403101d428906b1e1dd597551cd8ec51fde32c3383ce5a5f8f288eac0c0",
            "createdAt": "2021-07-02T07:12:56.012231726Z",
            "updatedAt": "2021-07-02T07:12:56.012231726Z",
            "keyId": "test-account",
            "tags": {
                "propose": "my-first-example"
            },
            "address": "0xce7801c24153afa215c5edb40f9aff6a793b1fe5",
            "disabled": false
        }
        ```

3. Sign a transaction using the Ethereum account:

    === "curl HTTP request"

        ```bash
        curl -X POST 'quorum-key-manager/stores/eth1-accounts/eth1/0xce7801c24153afa215c5edb40f9aff6a793b1fe5/sign-transaction' --header 'Content-Type: application/json' --data-raw '{"chainID": "0x1", "gasLimit": "0x5208", "gasPrice": "0x0", "data": "0xfeaeee", "nonce": "0x1", "to": "0x905B88EFf8Bda1543d4d6f4aA05afef143D27E18", "value": "0xfeaeae"}'
        ```

    === "JSON result"

        ```json
        0xf86501808252089490....
        ```
