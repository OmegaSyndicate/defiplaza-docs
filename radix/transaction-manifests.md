---
description: Interact with DefiPlaza on Radix without our frontend
---

# Transaction Manifests

One of the USPs of the Radix network is that communicating with the network can be done via human-readable instructions called Transaction Manifests. These manifests can be used to interact with DefiPlaza on Radix without the need to use our frontend, for example to build an arb bot, or if our frontend would be temporarily unavailable.

In all manifests the parameter that you have to replace are surrounded with `${}`, so to add your own account address you need to replace `${account}`.

### Swap

```
CALL_METHOD
  Address("${account}")
  "withdraw"
  Address("${tokenAddress}")
  Decimal("${tokenAmount}")
;

TAKE_ALL_FROM_WORKTOP
  Address("${tokenAddress}")
  Bucket("tokens")
;

CALL_METHOD
  Address("${DEX_COMPONENT_ADDRESS}")
  "swap"
  Bucket("tokens")
  Address("${counterTokenAddress}")
;

CALL_METHOD
  Address("${account}")
  "deposit_batch"
  Expression("ENTIRE_WORKTOP")
;

```

### Add Liquidity

To add liquidity, two scenarios are possible. If the single-side is in shortage, you need to add both tokens in ratio of the side. Otherwise you only have to add a single token.

#### Side is not in shortage

```
CALL_METHOD
  Address("${account}")
  "withdraw"
  Address("${tokenAddress}")
  Decimal("${tokenAmount}")
;

TAKE_ALL_FROM_WORKTOP
  Address("${tokenAddress}")
  Bucket("tokens")
;

CALL_METHOD
  Address("${DEX_COMPONENT_ADDRESS}")
  "add_liquidity"
  Bucket("tokens")
  None
  Some(Address("${baseTokenAddress}"))
;

CALL_METHOD
    Address("${account}")
    "deposit_batch"
    Expression("ENTIRE_WORKTOP")
;
```

#### Side is in shortage

```
CALL_METHOD
  Address("${account}")
  "withdraw"
  Address("${tokenAddress}")
  Decimal("${tokenAmount}")
;

CALL_METHOD
  Address("${account}")
  "withdraw"
  Address("${coTokenAddress}")
  Decimal("${coInputAmount}")
;

TAKE_ALL_FROM_WORKTOP
  Address("${tokenAddress}")
  Bucket("tokens")
;

TAKE_ALL_FROM_WORKTOP
  Address("${coTokenAddress}")
  Bucket("coTokens")
;

CALL_METHOD
  Address("${DEX_COMPONENT_ADDRESS}")
  "add_liquidity"
  Bucket("tokens")
  Some(Bucket("coTokens"))
  Some(Address("${baseTokenAddress}"))
;

CALL_METHOD
  Address("${account}")
  "deposit_batch"
  Expression("ENTIRE_WORKTOP")
;
```

#### Remove Liquidity

```
CALL_METHOD
    Address("${account}")
    "withdraw"
    Address("${tokenAddress}")
    Decimal("${tokenAmount}")
;

TAKE_ALL_FROM_WORKTOP
    Address("${tokenAddress}")
    Bucket("tokens")
;

CALL_METHOD
    Address("${DEX_COMPONENT_ADDRESS}")
    "remove_liquidity"
    Bucket("tokens")
;

CALL_METHOD
    Address("${account}")
    "deposit_batch"
    Expression("ENTIRE_WORKTOP");`
}
```
