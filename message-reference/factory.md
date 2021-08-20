---
description: >-
  This contract registers the relation between your token and others.It uses the
  pre-stored pair contract binary and instantiate it. So, you don’t have to
  execute pair contract additionally.
---

# Factory

### Transaction <a id="transaction"></a>

#### Create pair <a id="create-pair"></a>

Instantiate pair from uploaded WASM binary. Please check [this document](https://docs.terraswap.io/docs/howto/create_your_own_pair/) in detail usage.

```text
{
  "pair_code_id": "1",
  "token_code_id": "2",
  "init_hook": {
    "msg": "<base64_encoded_json_string>",
    "contract_addr": "<HumanAddr>"
  }
}
```

### Query <a id="query"></a>

#### Config <a id="config"></a>

```text
{
    "config": {}
}
```

#### Pair <a id="pair"></a>

```text
{
    "pair": {
        "asset_infos": [
            {
                "token": {
                    "contract_addr": "<HumanAddr>"
                }
            },
            {
                "native_token": {
                    "denom": "uluna"
                }
            }
        ]
    }
}
```

#### Pairs <a id="pairs"></a>

```text
{
    "pairs": {
        "start_after": [ //optional
            {
                "token": {
                    "contract_addr": "<HumanAddr>"
                }
            },
            {
                "native_token": {
                    "denom": "uluna"
                }
            }
        ],
        "limit": 10 //optional, default=10, max=30
    }
}
```



