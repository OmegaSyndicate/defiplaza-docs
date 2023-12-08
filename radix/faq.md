---
description: Frequently Asked Questions by our community
---

# FAQ

### Why do I need to add two tokens while DefiPlaza has single-sided liquidity?

Normally a pair has two sides, A and B. Say you add 100 to token A and 100 to token B. Someone buys some A, and you end up with 90 A and 110 B (this is a simplified example).

That is usually how it is supposed to be. But with single-sided liquidity, the LP provider of the token A now only has 90 A, and the other side has 110 B. That is unfair since the LP provider that provided the liquidity that was needed for the trade gets penalized.

So we set up our single-sided liquidity to use 2 pairs internally. One pair for token A has both A/B and the other pair for token B also has A/B.

Now the starting point is 100/0 and 0/100. When someone trades 10 to buy A, the balances are now 90/10 and 0/100. The single-sided liquidity is fairly distributed.&#x20;

But if you now want to add more liquidity to token A, you have to add 1/9th of token B to keep it fair for everybody. If we wouldn't do that, you would get too many LP tokens since we would only count token A and ignore the B part.

### **How is the APY calculated?**

Most APYs are calculated by taking the fee income over a few days and extrapolating that to a whole year.

DefiPlaza believes that Impermanent Loss is LP Providers' most significant net income killer and has developed the CALM algorithm to reduce the IL risk.&#x20;

Therefore, the APY on DefiPlaza is based on the standard calculations used to calculate IL:

* We take the balances of the pair of 14 days ago and multiply them by the current USD value of the tokens
* We take the current balances of the pair and multiply them by the current USD value of the tokens
* The difference is the IL and the APY since the fee income is part of the current balances.
