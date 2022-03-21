---
description: The center of interaction for the IGO
---

# Eternal Offering

## <mark style="color:blue;">Introduction</mark>

_<mark style="color:purple;">The EternalOffering.sol contract hosts the functionality used in the</mark>_ [_<mark style="color:purple;">Initial Gage Offering</mark>_](../../../products-services/gages/loyalty-gage/initial-gage-offering.md) _<mark style="color:purple;">event which users can participate in at launch.</mark>_&#x20;

<mark style="color:purple;">The Eternal Offering acts as a hybrid of the Eternal Factory and Treasury, holding ETRNL reserves to distribute ETRNL through the loyalty gages it deploys and provide liquidity using funds it receives from users. Note that the risk percentage for this IGO decreases by 5% for every quarter of the total ETRNL in the contract that is offered, starting with a value of 30% and ending with a value of 15%.</mark>

## Functions

### initialize

```
function initialize() external
```

Excludes the ETRNL/AVAX pairs and ETRNL/MIM pairs from rewards.

### viewTotalETRNLOffered

```
function viewTotalETRNLOffered() external view returns (uint256)
```

Returns the total amount of ETRNL offered in this IGO thus far.&#x20;

* `return: uint256` The total amount of ETRNL distributed in the offering

### viewTotalLp

```
function viewTotalLp() external view returns (uint256, uint256)
```

Returns the total amount of ETRNL/AVAX and ETRNL/MIM lp tokens acquired through the IGO thus far.

* `return: uint256` The total amount of ETRNL/AVAX lp tokens acquired through the IGO
* `return: uint256` The total amount of ETRNL/MIM lp tokens acquired through the IGO

### viewLiquidityOffered

```
function viewLiquidityOffered(address user) external view returns (uint256)
```

Returns the total amount of ETRNL a given user has been offered thus far through both gages and depositing.

* `user`: The address of the specified user
* `return: uint256` The total amount of ETRNL used by the user through this offering

### viewLiquidityDeposited

```
function viewLiquidityDeposited(address user) external view returns (uint256)
```

Returns the total amount of ETRNL a given user has been offered thus far solely through depositing.

* `user`: The address of the specified user
* `return: uint256` The amount of ETRNL used/offered to the user through depositing

### viewGage

```
function viewGage(uint256 id) external view returns (address)
```

Returns the address of a given loyalty gage created in this offering.

* `id`: The unique id of the specified gage
* `return: address` The address of the specified gage

### viewRisk

```
function viewRisk() public view returns (uint256 risk)
```

Returns the current risk percentage for loyalty gages.

### checkIndividualLimit

```
function checkIndividualLimit(uint256 amountETRNL, address user) public view returns (bool)
```

Evaluates whether the individual IGO limit is reached for a given user and amount of ETRNL to be offered.

* `amountETRNL`: The amount of ETRNL to be used for this specific offering
* `user`: The address of the specified user
* `return: boolean` True if the individual IGO limit is reached, otherwise false

### checkGlobalLimit

```
function checkGlobalLimit(uint256 amountETRNL) public view returns (bool)
```

Evaluates whether the global IGO limit is reached for a given amount of ETRNL to be offered.

* `amountETRNL`: The amount of ETRNL to be used for this specific offering
* `return: boolean` True if the global IGO limit is reached, otherwise false

### initiateEternalLoyaltyGage

```
function initiateEternalLoyaltyGage(uint256 amount, address asset) external payable
```

Creates an ETRNL loyalty gage contract for a given asset and amount.&#x20;

* `amount`: The amount of the asset to be used as deposit
* `asset`: The address of the specified asset

### settleGage

```
function settleGage(address receiver, uint256 id, bool winner) external
```

Settles a given loyalty gage closed by a given receiver. Only callable by an Eternal-deployed gage.

* `receiver`: The address of the specified receiver
* `id`: The unique id of the specified gage
* `winner`: Whether the gage closed in favor of the receiver or not

### provideLiquidity

Provides liquidity to either the MIM-ETRNL or AVAX-ETRNL pairs and sends ETRNL the message sender.

```
function provideLiquidity(uint256 amount, address asset) external payable
```

* `amount`: The amount of the asset being deposited
* `asset`: The address of the asset being deposited

### sendLPToTreasury

```
function sendLPToTreasury() external
```

Transfers all lp tokens, leftover ETRNL and any dust present in this contract to the Eternal Treasury.
