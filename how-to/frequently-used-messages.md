# Frequently Used Messages

### Transaction <a id="transaction"></a>

#### Provide liquidity / Withdraw <a id="provide-liquidity--withdraw"></a>

As the swap ratio is stated as [here](https://docs.terraswap.io/docs/introduction/mechanism/), the size of the pool is related with the difference of swap ratio. The ratio goes stable if the size of the pool increases, and vice versa. Otherwise, LP provider needs more tokens for adjusting the price in bigger pool. It means that the market loses elastic. LP provider adjusts this market by providing & withdraw the liquidity within this trade-off.

 **Provide liquidity**

Contribute to pool by sending sender’s token pair. Not only increasing its size, but also it affects to the swap ratio.

Execute this message by the **Pair contract** address!

```text
{
  "provide_liquidity": {
    "assets": [
      {
        "info" : {
            "token": {
                "contract_addr": "<HumanAddr>"
            }
        },
        "amount": "10"
      },
      {
        "info" : {
            "native_token": {
                "denom": "uluna"
            }
        },
        "amount": "10"
      }
    ]
  }
}
```

**Withdraw**

Withdraw your tokens and decrease the size of the pool.

Execute this message by the **Liquidity token contract** address! Not token contract, not pair contract neither!

```text
{
  "send": {
    "contract": "<PairContractAddress>",
    "amount": 123,
    "msg": "base64-encodedStringOfWithdrawMsg"
  },
}
```

In `send.msg`, you may decode this JSON string into base64 encoding.

```text
{
  "withdraw_liquidity": {}
}
```

Then, the liquidity token contract calculates the portion of your liquidity token comparing to the total supply, and withdraw the pairs.

### Query <a id="query"></a>

#### Pool <a id="pool"></a>

Pool query message returns the amount of the tokens in the pool from the given pair contract address.

```text
{
  "pool":{}
}
```

Response:

```text
{
  "height": "699536",
  "result": {
    "assets": [
      {
        "info": {
          "native_token": {
            "denom": "ukrw"
          }
        },
        "amount": "616618779506317"
      },
      {
        "info": {
          "native_token": {
            "denom": "uluna"
          }
        },
        "amount": "1407689375952"
      }
    ],
    "total_share": "29432943447776"
  }
}
```

#### Simulation / Reverse simulation <a id="simulation--reverse-simulation"></a>

Simulation works for guessing how much you will be swapped with your token.

If you want to know how much the target token will be given from source token, use `simulation`. Or if you want to derive the number of source token from the number of target token, use this query message.

**Simulation request**

```text
{
  "simulation": {
    "offer_asset": {
      "amount":"10000000",
      "info": {
        "native_token": {
          "denom":"uluna"
        }
      }
    }
  }
}
```

**Simulation request**

```text
{
  "height": "1274586",
  "result": {
    "return_amount": "2875706843",
    "spread_amount": "147593468",
    "commission_amount": "8653079"
  }
}
```

**Reverse simulation response**

```text
{
  "reverse_simulation":{
    "ask_asset": {
      "amount":"5000000000",
      "info": {
        "native_token": {
          "denom": "ukrw"
        }
      }
    }
  }
}
```

```text
{
  "height":"1274605",
  "result": {
    "offer_amount": "18070071",
    "spread_amount": "463716168",
    "commission_amount": "15045135"
  }
}
```





