# Create new Pair

When creating a new pair on RadIxPlaza, an amount of base tokens and DFP2 must be provided, which will be **donated** to the protocol.

This minimum amount of liquidity is used to prevent the pair from ever running empty, which could lead to price manipulation.

Only one pair per base token can be created. It is not possible for example to create two XRD/DFP2 pairs.

Pairs that are created are not updateable, so fees and concentration levels of new pairs are fixed. At the moment a default of of 0.15% is set for each pair and a concentration of X and Y, based on benchmarks as explained in our [White Paper](../../introduction/white-papers.md). We might allow different configurations in the future to be set via our UI.

### Pair Governance

The DefiPlaza DAO can delist pairs that might harm the normal operation of the DEX. Examples are:

* Pairs created with a price of base token in DFP2 which is far away from the market price.
* \[..]
