---
description: JSON-RPC node proxy tutorial
---

# Connect to the JSON-RPC node proxy

This tutorial walks you through connecting to the JSON-RPC node proxy and signing an Ethereum transaction using Quorum Key Manager.

## Prerequisites

- Quorum Key Manager installed
- [`curl` command line](https://curl.se/download.html)
- An [Azure Key Vault](https://azure.microsoft.com/en-us/services/key-vault/) configured

## Steps

1. In the Quorum Key Manager [manifest file], specify an `Eth1Account` store to allocate your Azure keys, and specify the
   RPC node to connect to.
   Use the following template, filling in the `specs` for `AzureKeys` with [information about your Azure Key Vault]:

    ```yaml
    - kind: Eth1Account
      version: 0.0.1
      name: eth1-accounts
      specs:
        keystore: AzureKeys
        specs:
          vaultName: <AZURE-VAULT-ID>
          tenantID: <TENANT-ID>
          clientID: <CLIENT-ID>
          clientSecret: <SECRET>

    - kind: Node
      name: quorum-node
      version: 0.0.0
      specs:
        rpc:
          addr: http://quorum1:8545
        tessera:
          addr: http://tessera1:9080
    ```

2. Run Quorum Key Manager with the manifest file loaded, using the [`--manifest-path`](../Reference/CLI-Syntax.md#manifest-path) option:

    ```bash
    quorum-kms run --manifest-path=<PATH-TO-MANIFEST-FILE>
    ```

3. Create an Ethereum account:

    === "curl HTTP request"

        ```bash
        curl -X POST 'quorum-key-manager/stores/eth1-accounts/eth1'
        ```

    === "JSON result"

        ```json
        {
            "publicKey": "0x045c36d8acc9b00a33221cea6caa39a826e396c0be9df00d224c7aa077b4b58a18e6fdf79a4e9724f9f61a8cdac691c3fea30309be0f46035e299051e4c95a62b3",
            "compressedPublicKey": "0x035c36d8acc9b00a33221cea6caa39a826e396c0be9df00d224c7aa077b4b58a18",
            "createdAt": "2021-07-02T07:33:26.24350701Z",
            "updatedAt": "2021-07-02T07:33:26.24350701Z",
            "expireAt": "0001-01-01T00:00:00Z",
            "keyId": "qkm--95BdaiyQ8OEyX8a",
            "address": "0xd8c88f28748367a11d3c6fc010eef7b670ac016f",
            "disabled": false
        }
        ```

4. Sign a transaction using the Ethereum account and the RPC node proxy:

    === "curl HTTP request"

        ```bash
        curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_sendTransaction","params":[{"from": "0xd8c88f28748367a11d3c6fc010eef7b670ac016f","to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567", "data":"0xafed"}], "id":1}' quorum-key-manager/nodes/quorum-node
        ```

    === "JSON result"

        ```json
        {"jsonrpc":"2.0","result":"0x8c961ba2c3f51f9088e1a12a81bb1ad9c551ccfad75615f39e4fc95c3bb7086b","error":null,"id":1}
        ```
