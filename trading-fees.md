# Trading Fees

Each liquidity pool for whitelisted asset pair has **LP Commission** rates that is paid as a trading fee outside of spread determined by algorithmic price-making. In LoopSwap, LP Commission is fixed at _0.3%_ and are paid from the trader’s received asset from the transaction.

> Additionally, if the traded asset is a native token such as UST, the Terra network will incur a tax on the transfer \(not controlled by LoopSwap contract\).

$$
received = Bout(1-feeLP)-tax
$$

LP Commission paid in each trade goes back into to the corresponding liquidity pool as fee for liquidity providers. LP Commission which is accumulated to the pool can be withdrawn by burning LP tokens, which are generated from liquidity provision.



