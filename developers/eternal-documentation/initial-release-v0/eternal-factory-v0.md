---
description: The gage factory and second brain of the treasury
---

# Eternal Factory V0

## <mark style="color:blue;">Introduction</mark>

_<mark style="color:purple;">The EternalFactory.sol contract is responsible for creating new gage contracts before relaying any remaining financial activity (related to any gage) to the Eternal Treasury.</mark>_&#x20;

<mark style="color:purple;">This contract is ownable and owned by the Eternal Fund. The Eternal Factory maintains the</mark> [<mark style="color:purple;">circular flow of ETRNL</mark>](../../../token/tokenomics/#circular-flow-of-etrnl) <mark style="color:purple;">and sustainability of the system by keeping the inflowing ETRNL at a level greater than or equal to that of the outflowing ETRNL. This is mainly done by the calculation of a dynamic limit determined by the limiting variable,</mark> $$\psi$$<mark style="color:purple;">.  The factory also holds the pre-determined risk percentages for any given asset type, as well as numerous other constants, factors and estimates it uses to calculate gage conditions. Last, the Eternal Factory contract acts as the central unit with regards to processing the transaction data received from the Eternal Token contract and ultimately calculating the daily ETRNL transactions subject to fees,</mark> $$\alpha$$<mark style="color:purple;">.</mark>

## Functions

### initialize

```
function initialize(address _treasury, address _fund) external onlyAdmin
```

Initializes constants, factors and limiting variables as well as the Eternal Treasury interface and attributes "fund rights" to the Timelock contract. Only callable by the temporary admin.

* `_treasury`: The address of the initial Eternal Treasury contract
* `_fund`: The address of the Timelock contract

### initiateEternalLiquidGage

```
function initiateEternalLiquidGage(address asset, uint256 amount) external payable override
```

Creates an Eternal liquid gage using a given asset and amount. The user must give the Eternal Factory sufficient allowance to move their funds.

* `asset`: The address of the asset being deposited to the gage by the user
* `amount`: The amount of the asset being deposited

### updateCounters

```
function updateCounters(uint256 amount) external
```

Updates any 24h counters related to ETRNL in/outflow. Only callable by the Eternal Token contract.

* `amount`: The amount by which the 24h counter must be updated by

### gageLimitReached

```
function gageLimitReached(address asset, uint256 amountAsset, uint256 risk) public view returns (bool limitReached)
```

Computes whether there is enough ETRNL left in the treasury to allow for a given liquid gage (whilst remaining sustainable).

* `asset`: The address of the asset to be deposited to the specified liquid gage
* `amountAsset`: The amount of the asset being deposited to the specified liquid gage
* `risk`: The current risk percentage for an Eternal liquid gage with this asset as deposit
* `return: boolean` True if the gaging limit is reached, false otherwise

### percentCondition

```
function percentCondition() public view returns (uint256)
```

Computes a percent condition for a given Eternal gage.

* `return: uint256` The amount by which the ETRNL supply must deflate before the gage closes in favor of the receiver

### setEternalTreasury

```
function setEternalTreasury(address newContract) external onlyFund
```

Updates the address of the Eternal Treasury contract. Only callable by governance.

* `newContract`: The address of the new Eternal Treasury

### setEternalToken

```
function setEternalToken (address newContract) external onlyFund
```

Updates the address of the Eternal Token contract. Only callable by governance.

* `newContract`: The address of the new Eternal Token

## Events

### NewGage

```
event NewGage(uint256 id, address indexed gageAddress)
```

Signals the deployment of a new gage with a given unique id and address.
