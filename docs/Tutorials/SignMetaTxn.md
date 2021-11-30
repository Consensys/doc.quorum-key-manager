---
Description: How to sign a meta-transaction with QKM and send to Infura ITX
---

# Sign a meta-transaction

This tutorial walks you through signing a meta-transaction with Quorum Key Manager (QKM) and sending it to Infura
Transactions (ITX).
This tutorial is an extension of the [Connect to an Infura endpoint tutorial](ConnectInfura.md) and uses the Rinkeby testnet.

## Prerequisites

Follow steps 1 to 5 in the [Connect to an Infura endpoint tutorial](ConnectInfura.md).
This should give you an Ethereum account with a new address.

## Steps

1. Fund your Ethereum account.
   For example, you can go to the [Rinkeby faucet](https://www.rinkeby.io/#faucet) and follow the instructions there.
   You can use [Etherscan](https://etherscan.io/) to check that the faucet gave you ETH.

1. Deposit ETH into the Infura deposit contract using QKM `infura-node`.
   The following example uses the sample deposit contract `0x015C7C7A7D65bbdb117C573007219107BD7486f9`:

    === "curl HTTP request"

        ```bash
        curl --location --request POST 'https://localhost:8080/nodes/infura-node' \
            --header 'Authorization: Basic YWRtaW4tdXNlcg==' \
            --header 'Content-Type: application/json' \
            --data-raw '{"jsonrpc":"2.0","method":"eth_sendTransaction",
                "params":[
                    {"from": "<MY_ETH_ACCOUNT_ADDRESS>",
                    "to": "0x015C7C7A7D65bbdb117C573007219107BD7486f9",
                    "gas": "0x65000",
                    "gasPrice": "0x1000000000",
                    "value": "0x1000000000000000"}
                    ], "id":3
                }
                '
        ```

    === "JSON result"

        ```bash
        {
            "jsonrpc": "2.0",
            "result": "0xff1bd105d7254789b6fc5e18639e2395068108d66bcfe728e5f792295b7526be",
            "error": null,
            "id": 3
        }
        ```

    The response should yield the transaction hash for the successful deposit.
    You can use [Etherscan](https://etherscan.io/) to check that the deposit went through:

    ![Etherscan deposit](../Images/EtherscanDeposit.png)

1. Build a message to be sent to a test contract.
   In this example, the message says `Hello world!, 6210 was here`, which translates to the following Ethereum message:

    ```text
    0xf15da7290000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000001b48656c6c6f20776f726c64212c20366c32302077617320686572650000000000
    ```

    The hash of the Ethereum message is:

    ```text
    bf11b3f509e51cbb52070358c5bfadd9047ee9750e865f8f1b1ad125df65e853
    ```
