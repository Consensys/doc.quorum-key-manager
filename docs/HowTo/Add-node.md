---
description: Add Node using manifest
---

# Add Node to Quorum Key Manager

On every defined node Quorum Key Manager will exposed an HTTP and Websocket endpoints to interact with the nodes
using Quorum Key Manager Ethereum Stores as remote and secure keystores.

## Sample manifest

Next you can find two examples of how to add a Besu and Quorum+Tessera nodes:

```
    # GoQuorum node manifest
    - kind: Node
      version: 0.0.0
      name: goquorum-node
      specs:
        rpc:
          addr: http://goquorum1:8545
        tessera:
          addr: http://tessera1:9080

    # Besu node manifest
    - kind: Node
      version: 0.0.0
      name: besu-node
      specs:
        rpc:
          addr: http://validator1:8545
```
