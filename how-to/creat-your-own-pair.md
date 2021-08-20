# Creat Your Own Pair

### How to create your own pair <a id="how-to-create-your-own-pair"></a>

A pre-stored pair is used in this procedure. Token contract should be instantiated in advance.

The JSON parameter of instantiation is as below:

```text
{
  "pair_code_id": "1",
  "token_code_id": "2",
  "init_hook": {
    "msg": "base64_encoded_json_data",
    "contract_addr": "terra..."
  }
}
```

The factory contract is responsible for creation of LoopSwap pair as well as being the directory for all pairs. You may input numbers corresponding to `pair_code_id` and `token_code_id`. The token contract address is used for `init_hook.contract_addr`.

To set `init_hook.msg`, you must first organize another JSON as below:

```text
{
  "create_pair": {
    "asset_infos": [
      {
        "token": {
          "contract_address": "terra..."
        }
      },
      {
        "native_token": {
          "denom": "uusd"
        }
      }
    ]
  }
}
```

This is a JSON constructor of pair contract.

* A token pair can be either, contract-based token, or terra-native token
  * `asset_infos[x].token.contract_addr`: Contract-basd token **address** is entered here.
  * `asset_infos[x].native_token.denom`: Terra native token **denominator** is entered here.

After completing the JSON, you may convert the JSON into Base64 encoding.

```text
{
  "create_pair": {
    "asset_infos": [
        {
            "token": {
                "contract_addr": "terra..."
            }
        },
        {
            "native_token": {
                "denom": "uusd"
        }
      }
    ]
  }
}
```

Base64 encoded string will look something like the below:

```text
ew0KICAgICJhc3NldF9pbmZvcyI6IFsNCiAgICAgICAgew0KICAgICAgICAgICAgInRva2VuIjogew0KICAgICAgICAgICAgICAgICJjb250cmFjdF9hZGRyIjogInRlcnJhdG9rZW5hZGRyMDAwMXh4eHh4eHh4Ig0KICAgICAgICAgICAgfQ0KICAgICAgICB9LA0KICAgICAgICB7DQogICAgICAgICAgICAibmF0aXZlX3Rva2VuIjogew0KICAgICAgICAgICAgICAgICJkZW5vbSI6ICJ1bHVuYSINCiAgICAgICAgICAgIH0NCiAgICAgICAgfQ0KICAgIF0sDQogICAgImNvbW1pc3Npb25fY29sbGVjdG9yIjogInRlcnJhY29tbWlzc2lvbmNvbGxlY3RvcjAwMDF4eHh4eHh4eCIsDQogICAgImxwX2NvbW1pc3Npb24iOiAiMC4zIiwNCiAgICAib3duZXIiOiAidGVycmF0b2tlbmNvbnRyYWN0b3duZXIwMDAxeHh4eHh4eHh4eCIsDQogICAgIm93bmVyX2NvbW1pc3Npb24iOiAiMC4yIiwNCiAgICAidG9rZW5fY29kZV9pZCI6IDENCn0=
```

Copy this encoded string into `init_hook.msg` of the JSON, which was provided at the top of this section.

```text
{
  "pair_code_id": "1",
  "token_code_id": "2",
  "init_hook": {
    "msg": "ew0KICAgICJhc3NldF9pbmZvcyI6IFsNCiAgICAgICAgew0KICAgICAgICAgICAgInRva2VuIjogew0KICAgICAgICAgICAgICAgICJjb250cmFjdF9hZGRyIjogInRlcnJhdG9rZW5hZGRyMDAwMXh4eHh4eHh4Ig0KICAgICAgICAgICAgfQ0KICAgICAgICB9LA0KICAgICAgICB7DQogICAgICAgICAgICAibmF0aXZlX3Rva2VuIjogew0KICAgICAgICAgICAgICAgICJkZW5vbSI6ICJ1bHVuYSINCiAgICAgICAgICAgIH0NCiAgICAgICAgfQ0KICAgIF0sDQogICAgImNvbW1pc3Npb25fY29sbGVjdG9yIjogInRlcnJhY29tbWlzc2lvbmNvbGxlY3RvcjAwMDF4eHh4eHh4eCIsDQogICAgImxwX2NvbW1pc3Npb24iOiAiMC4zIiwNCiAgICAib3duZXIiOiAidGVycmF0b2tlbmNvbnRyYWN0b3duZXIwMDAxeHh4eHh4eHh4eCIsDQogICAgIm93bmVyX2NvbW1pc3Npb24iOiAiMC4yIiwNCiAgICAidG9rZW5fY29kZV9pZCI6IDENCn0=",
    "contract_addr": "terra..."
  }
}
```

Factory contract is instantiated and a new pair is created.

