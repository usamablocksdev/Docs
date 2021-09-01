---
description: >-
  This site hosts guides, FAQs, and documentation produced through the joint
  efforts of the community and the Loop team.
---

# 👋 Intro to Loop

## Swap <a id="swap"></a>

Swap in LoopSwap works as same as trade in other exchanges. Price of centralized exchanges for both stock and cryptocurrency move by price bidding system, and supply & demand. These prices change in millisecond intervals, so real-time transaction is maintained in the market. But if anyone is trying to implement an exchange with the bidding-based pricing on blockchain, immediate execution of transaction becomes impossible due to block time.

Therefore, a different pricing approach is used in LoopSwap - algorithmic pricing by tracking the ratio of the paired asset within the liquidity pool. To learn more about this approach, please refer to [mechanism section](https://app.gitbook.com/@usama-zeeyou/s/loop/~/drafts/-MiV9TLqqmMLvhM7R-9J/mechanism).

### Prerequisites <a id="prerequisites"></a>

* Token & pair should be deployed
* You should know the addresses of token & pair.
* Increase your allowance. [Execute `IncreaseAllowance`](https://app.gitbook.com/@usama-zeeyou/s/loop/message-reference/cw20-token)

### Swap by using CLI <a id="swap-by-using-cli"></a>

####  \(Native token, Contract-minted token\) -&gt; Contract-minted Token <a id="native-token-contract-minted-token---contract-minted-token"></a>

By command line, all transactions can be executed in this way:

```text
loopcli tx wasm execute <contract-address> <handle-msg> <coins>
```

* `contract-address`: In swap transaction, this should be the pair address.
* `handle-msg`: It represents the method and parameters of this execution. Will explain below.
* `coins`: Fee to execute transaction

Enter `contract-address`, `coins` and `handle-msg`. To learn more about the general rules for `handle-msg` please refer to this [link](https://docs.terraswap.io/docs/howto/query/).

* Source asset: native token

```text
{
    "swap": {
        "offer_asset": {
            "info" : {
                "native_token": {
                    "denom": "uluna"
                }
            },
            "amount": "10"
        },
        "to": "<HumanAddr>"
    }
}
```

* Source asset: contract-minted token

```text
{
    "swap": {
        "offer_asset": {
            "info" : {
                "token": {
                    "contract_addr": "<HumanAddr>"
                }
            },
            "amount": "10"
        },
        "to": "<HumanAddr>"
    }
}

```

`swap.offer_asset` represents your source asset. Please make sure that `swap.offer_asset.amount` is not same as your amount. It depends on the decimal of the token setting. In case of Luna, its decimal is 9. Then, if `swap.offer_asset.amount` reads `10`, the actual amount is `10 x 10^-9`. So, you should multiply with mathcing value, `10^(decimal)`.

`swap.to` is the destination token address. It is unnecessary to enter the amount to swap into, since LoopSwap price is calculated algorithmically.

After filling it out, you may choose to change it into an inline string \(not necessary if you can make it with multiline\):

```text
'{"swap":{"offer_asset": {"info" : {"token": {"contract_addr": "<HumanAddr>"}},"amount": "10"},"to": "<HumanAddr>",}}'
```

This is your `handle-msg`. The `handle-msg` can be used to complete the CLI command to swap tokens.

####  Contract-minted token -&gt; Native Token <a id="contract-minted-token---native-token"></a>

Swapping contract-minted token to native token is executed with the same logic as above, but requires a differnet `handle-msg` due to difference in token system and its implementation. Message looks like:

```text
{
    "send": {
        "contract": "<HumanAddr>",
        "amount": "10",
        "msg": Binary({
            "swap": {}
        })
    }
}
```

The method is a little bit tricky. Please do not lose your concentration!

```text
terracli tx wasm execute <contract-address> <handle-msg> <coins>
```

In the CLI,

* `contract-address`: Enter **token address**

In the message:

* `send.contract`: Enter **pair address**
* `send.amount`: The amount of the origin token to swap from

`send.msg.swap` is an optional value, which is not required for basic swap executions.

Encode `{"swap":{}}` into base64 encoding. It should look something like: `eyJzd2FwIjp7fX0=`.

Enter the base64 encoded value for `msg` of the JSON:

```text
{
    "send": {
        "contract": "<HumanAddr>",
        "amount": "10",
        "msg": "eyJzd2FwIjp7fX0="
    }
}
```

After then, you may proceed as like the above.

