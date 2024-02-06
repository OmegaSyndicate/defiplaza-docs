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

Instead of APY DefiPlaza uses something we call Annualized liquidity return (ALR).

Annualized liquidity return (ALR) is a metric that measures the difference in supplying liquidity into a certain pool with respect to just holding the token for that pool. It is measured in percent per year. For example, if the ASTRL / DFP2 pool has an ALR of 5% for the base pool and 6% for the quote pool, that means LPs in the base pool have seen their LP token value (measured in ASTRL) increase at an annualized rate of 5%. The LPs for the quote pool have seen their LP token value (measured in DFP2) increase at an annualized rate of 6%.\


The idea of this metric is to allow users to see how well the pool has performed historically as compared to just keeping the token in your wallet. It is the added value from providing liquidity, considering impermanent loss (IL). If impermanent loss is larger than trade/fee income, the ALR can be negative. Multiple time periods are given, such that you can view how well the pool has performed since inception as well as over a recent period.

A purely educational example of a 7-day ALR calculation is given below:

**7 days ago:**

Market price 1 DFP2 per ASTRL\
Base LP value - 100 ASTRL (=100 ASTRL) \
Quote LP value - 90 DFP2 + 10 ASTRL (=100 DFP2)

**Today:**

Market price 1.2 DFP2 per ASTRL\
Base LP value - 90 ASTRL + 14 DFP2 (=101.67 ASTRL)\
Quote LP value - 101 DFP2 (=101 DFP2)

Base return = 1.67% per week, which annualizes to +136.7%\
Quote return = 1% per week, which annualizes to +68%
