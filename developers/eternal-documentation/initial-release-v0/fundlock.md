---
description: A slightly complex token vesting mechanism
---

# FundLock

## <mark style="color:blue;">Introduction</mark>

_<mark style="color:purple;">The FundLock.sol contract implements a</mark>_ [_<mark style="color:purple;">token vesting mechanism used by seed/private investors</mark>_](../../../token/tokenomics/tokenomics.md#seed-private-investor-vesting-schedules)_<mark style="color:purple;">.</mark>_

<mark style="color:purple;">Upon initialization, a designated recipient address is provided to the FundLock contract. This address will receive any funds withdrawn from it. For the Initial Release V0, two FundLock contracts are deployed: one for seed investors, the other for private investors.</mark>

## Functions

### viewAmountAvailable

```
function viewAmountAvailable() public view returns (uint256)
```

View the amount of tokens available for withdrawal based on the amount the supply has decreased by.

* `return: uint256` The maximum amount of tokens available to be withdrawn by investors from this contract at this time

### withdrawFunds

```
function withdrawFunds() external
```

Withdraws an amount of the locked funds proportional to the deflation of the Eternal Token to the designated address.&#x20;
