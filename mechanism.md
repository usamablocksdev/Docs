# Mechanisms

### Liquidity Pools <a id="liquidity-pools"></a>

LoopSwap creates automated markets for pairs of tokens \(or native Loop coins like UST\) called **pools** which enable users to exchange one asset for the other directly on-chain. Pools maintain balances of both assets, to which users can provide liquidity in exchange for reward-bearing LP tokens. A more detailed explanation about LP tokens and their relationship with LoopSwap can be found in the Uniswap docs

### Constant Product

LoopSwap pools make prices based on a **constant product invariant.**

$$
XY=k
$$

The product of the number of tokens on each side of the pool should remain constant across trading operations \(buying / selling\).

### Pricing <a id="pricing"></a>

In order to preserve the constant product invariant, **LoopSwap** will make prices that ensure the product of resultant balances of the pool is as close as possible to product calculated prior to the trade. With XXX being the current balance of the pool’s source asset and and YYY being that of the target asset:

$$
XY=k=(X+Ain​)(Y−Bout​)
$$

To determine the proper value of BoutB_{out}Bout​ given the trader’s offered asset AinA_{in}Ain​ :

$$
Bout​=Y Ain/X+Ain
$$

LoopSwap is able to execute trades with only the current balances of the pool and the number of incoming tokens. The market price is encoded the number of pool’s target tokens divided by the source asset \(also called the pool ratio\). The spread between the executed and the expected trade is:

$$
sprea=max(Y Ain/X+Ain - YAin/X,0)
$$

When a pool has large balances of tokens on both sides from liquidity providers, the spread becomes smaller and helps the pool execute closer to its reported price of Y/X.

### Farm <a id="pricing"></a>

LoopSwap provides different [Farm](https://app.gitbook.com/@usama-zeeyou/s/loop/how-to/farming) depending on the pairs against which we have provide liquidity. You can stake your LP tokens in the respective farm and earn some reward in the form of **LOOP**

### Stake <a id="pricing"></a>

LoopSwap also comes up with the facility of direct staking of the **LOOP** tokens from which you can earn the rewad in the fom of **LOOP** daily. 



