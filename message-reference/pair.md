# Pair

### Transaction <a id="transaction"></a>

#### Provide liquidity <a id="provide-liquidity"></a>

Send user’s asset to a LoopSwap contract and provide liquidity.  
 **NOTE: You should** [**allow your allowance**](https://app.gitbook.com/@usama-zeeyou/s/loop/~/drafts/-MiV9TLqqmMLvhM7R-9J/message-reference/cw20-token) **of the token before providing liquidity!**

Asset can be both of contract-based token and native token. It can be distinguished with the key under `info`: `token` or `native_token`.

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
    ],
    "slippage_tolerance": 0.1 // optinonal
  }
}
```

#### Swap <a id="swap"></a>

Swap between the given two tokens. It can be thought of as trade.  
 `offer_asset` is your source asset and `to` is your destination token contract.

**NOTE: You should** [**allow your allowance**](https://app.gitbook.com/@usama-zeeyou/s/loop/~/drafts/-MiV9TLqqmMLvhM7R-9J/message-reference/cw20-token) **of the token before swap!!**  
 **NOTE: This method is only used to swap to contract-based token as a destination! In opposite case, please check** [**another document**](https://app.gitbook.com/@usama-zeeyou/s/loop/~/drafts/-MiV9TLqqmMLvhM7R-9J/how-to/swap)

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
        "belief_price": 0.1,  // optional
        "max_spread": 0.1, // optional
        "to": "<HumanAddr>",
    }
}
```

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
        "belief_price": 0.1,  // optional
        "max_spread": 0.1, // optional
        "to": "<HumanAddr>" // optional,
    }
}

```

### Query <a id="query"></a>

#### Pool <a id="pool"></a>

```text
{
    "pool": {}
}
```

#### Simulation <a id="simulation"></a>

```text
{
    "simulation": {
        "offer_asset": {
            "info" : {
                "token": {
                    "contract_addr": "<HumanAddr>"
                }
            },
            "amount": "10"
        }
    }
}
```

#### Reverse simulation <a id="reverse-simulation"></a>

```text
{
    "reverse_simulation": {
        "ask_asset": {
            "info" : {
                "token": {
                    "contract_addr": "<HumanAddr>"
                }
            },
            "amount": "10"
        }
    }
}
```

