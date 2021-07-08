---
description: Signing an Ethereum transaction tutorial
---

# Sign Ethereum Transaction

You can create an Ethereum account and sign a transaction with Quorum Key Manager.

## Prerequisites

- Quorum Key Manager installed
- [`curl` command line](https://curl.se/download.html)

## Steps

1. Specify in our setting of Quorum Key Manager(QKM) service that we want to create an `Eth1Account` Store where our keys will be allocated in Hashicorp.
   For that we will need to create a manifest file with the following content:

    ```yaml
    kind: Eth1Account
    version: 0.0.1
    name: eth1-accounts
    specs:
      keystore: HashicorpKeys
      specs:
        mountPoint: {{STORAGE_MOUNTING_POINT}}
        address: {{SERVER_URL}}
        token: {{MY_API_TOKEN}}
        namespace: {{SELECTED_NAMESPACE}}
    ```

2. Once we initialize our QKM loading above manifest we can create an account via HTTP as follow:

    ```bash
    curl -X POST '{{QUORUM_KEY_MANAGER_URL}}/stores/eth1-accounts/eth1' --header 'Content-Type: application/json' --data-raw '{"keyId": "test-account", "tags": {"propose": "my-first-example"}}'
    ```

    We will obtain back the ethereum account:

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

3. Now we can sign an ethereum transaction using the account we just created:

    ```bash
    curl -X POST '{{QUORUM_KEY_MANAGER_URL}}/stores/eth1-accounts/eth1/0xce7801c24153afa215c5edb40f9aff6a793b1fe5/sign-transaction' --header 'Content-Type: application/json' --data-raw '{"chainID": "0x1", "gasLimit": "0x5208", "gasPrice": "0x0", "data": "0xfeaeee", "nonce": "0x1", "to": "0x905B88EFf8Bda1543d4d6f4aA05afef143D27E18", "value": "0xfeaeae"}'
    ```

    As answer we get the signed transaction data:

    ```json
    0xf86501808252089490....
    ```
