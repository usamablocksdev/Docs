# CW20 Token

### Transaction <a id="transaction"></a>

#### Transfer <a id="transfer"></a>

Transfer token from the sender user to the recipient.

```text
{
    "transfer": {
        "recipient": "<HumanAddr>",
        "amount": 123123,
    }
}
```

#### Burn <a id="burn"></a>

Burn tokens from total supply.

```text
{
    "burn": {
        "amount": 123123
    }
}
```

####  Send <a id="send"></a>

Work same as transfer but it sends token to contract, not user address.  
 And, it triggers given message in `msg`. The given message should be executable on recipient contract.

`msg` is base64-endcoded JSON string.

```text
{
    "send": {
        "contract": "<HumanAddr>",
        "amount": 123123,
        "msg": "1234erwfaffaesfaef="
    }
}
```

#### Mint <a id="mint"></a>

It produces token and transfer to given recipient.

```text
{
    "mint": {
        "recipient": "<HumanAddr>",
        "amount": 123123
    }
}
```

#### Increase/Decrease allowance <a id="increasedecrease-allowance"></a>

It increases / decreases allowance of withdrawable token from the executor.  
 After execution, user token can be transferred by spender’s contract method execution, not only `transfer`.

And it expires on the given time point.

```text
{
    "increase_allowance": {
        "spender": "<HumanAddr>",
        "amount": 123123,
        "expires": {
            "at_height": 123123,
            // or
            "at_time": 123123,
            // or
            "never": {}
        }
    }
}
```

```text
{
    "decrease_allowance": {
        "spender": "<HumanAddr>",
        "amount": 123123,
        "expires": {
            "at_height": 123123,
            // or
            "at_time": 123123,
            // or
            "never": {}
        }
    }
}
```

#### Transfer from / send from <a id="transfer-from--send-from"></a>

It transfers token from owner to recipient, which not owner nor recipeint are not the contract executor. Before execution, the allowance should be increased.

```text
{
    "transfer_from": {
        "owner": "<HumanAddr>",
        "recipient": "<HumanAddr>",
        "amount": 123123,
    }
}
```

```text
{
    "send_from": {
        "owner": "<HumanAddr>",
        "recipient": "<HumanAddr>",
        "amount": 123123,
        "msg": "<base64_encoded_json_message>"
    }
}

```

####  Burn from <a id="burn-from"></a>

Burns token from token supply, whose owner is not same as the contract executor.

```text
{
    "burn_from": {
        "owner": "<HumanAddr>",
        "amount": 123123
    }
}
```

### Query <a id="query"></a>

#### Get balance <a id="get-balance"></a>

Check the balance of the given address

```text
{
    "balance": {
        "address": "<HumanAddr>"
    }
}
```

####  Token info <a id="token-info"></a>

Check metadata of the contract.

 It check:

* Name
* Decimals
* Total supply
* Other useful information

```text
{
    "token_info": {}
}
```

#### Get minter <a id="get-minter"></a>

```text
{
    "minter": {}
}
```

#### Get allowance <a id="get-allowance"></a>

Get allowance list of the given owner & spender.

```text
{
    "allowance": {
        "owner": "<HumanAddr>",
        "spender": "<HumanAddr>"
    }
}
```

#### Get all allowance <a id="get-all-allowance"></a>

Get list of all allowance of the token.

```text
{
    "all_allowances": {
        "owner": "<HumanAddr>",
        "start_after": "<HumanAddr>", // optional
        "limit": 1 // optional
    }
}
```

####  Accounts list that have the token <a id="accounts-list-that-have-the-token"></a>

Get all accounts list of the token holder.

```text
{
    "all_accounts": {
        "start_after": "<HumanAddr>", // optional
        "limit": 1 // optional
    }
}
```

