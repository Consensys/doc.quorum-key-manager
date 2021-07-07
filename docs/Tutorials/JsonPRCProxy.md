---
description: JSON-RPC node proxy tutorial
---

# Connect to the JSON-RPC node proxy

You can connect to the JSON-RPC proxy using a Quorum Key Manager remote keystore.

## Prerequisites

- Quorum Key Manager installed

Firstly we need to specify in our setting of Quorum Key Manager(QKM) that we want to create an `Eth1Account` Store to allocate our keys
and the rpc node we want to connect to. For that we will need to create a manifest file with the following content:

```yaml
- kind: Eth1Account
  version: 0.0.1
  name: eth1-accounts
  specs:
    keystore: AKVKeys
    specs:
      vaultName: {{AKV_VAULT_ID}}
      tenantID: {{TENANT_ID}}
      clientID: {{CLIENT_ID}}
      clientSecret: {{SECRET}}

- kind: Node
  name: quorum-node
  version: 0.0.0
  specs:
    rpc:
      addr: http://quorum1:8545
    tessera:
      addr: http://tessera1:9080
```

Once we initialize our QKM loading above manifest we can create an account via HTTP as follow:

```bash
curl -X POST '{{QUORUM_KEY_MANAGER_URL}}/stores/eth1-accounts/eth1'
```

We will obtain back the ethereum account:

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

Now we are going to sign a transaction using the rpc node proxy defined above and using the account we just created:

=== "curl HTTP request"

    ```bash
    curl -H "Content-Type: application/json" -X POST --data '{"jsonrpc":"2.0","method":"eth_sendTransaction","params":[{"from": "0xd8c88f28748367a11d3c6fc010eef7b670ac016f","to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567", "data":"0xafed"}], "id":1}' {{QUORUM_KEY_MANAGER_URL}}/nodes/quorum-node
    ```

=== "JSON result"

    ```json
    {"jsonrpc":"2.0","result":"0x8c961ba2c3f51f9088e1a12a81bb1ad9c551ccfad75615f39e4fc95c3bb7086b","error":null,"id":1}
    ```
