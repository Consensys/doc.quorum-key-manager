---
description: Nodes concept page
---

# Nodes

A node is a Quorum Key Manager (QKM) component that interfaces with underlying node endpoints (such as Ethereum RPC nodes and Tessera nodes).

You can configure a node using a [node manifest](../HowTo/Use-Manifest-File/Node.md), which
includes the configuration to [connect to the JSON-RPC node proxy](../Tutorials/JsonRPCProxy.md).

When connected to the JSON-RPC node proxy, QKM intercepts the following methods for performing remote transaction signing:

- [`eea_sendTransaction`](https://entethalliance.github.io/client-spec/spec.html#sec-eea-sendTransaction)
- [`eth_accounts`](https://ethereum.github.io/execution-apis/api-documentation/)
- [`eth_sendTransaction`](https://ethereum.github.io/execution-apis/api-documentation/)
  ([the GoQuorum version](https://docs.goquorum.consensys.net/en/latest/Reference/API-Methods/#eth_sendtransaction) is also supported.)
- [`eth_sign`](https://ethereum.github.io/execution-apis/api-documentation/)
- [`eth_signTransaction`](https://ethereum.github.io/execution-apis/api-documentation/)
