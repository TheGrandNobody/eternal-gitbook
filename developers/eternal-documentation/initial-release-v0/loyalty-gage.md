---
description: The blueprint for all loyalty gages
---

# Loyalty Gage

## <mark style="color:blue;">Introduction</mark>

_<mark style="color:purple;">The LoyaltyGage.sol contract represents the standard implementation for any given gage to fall under the category of</mark>_ [_<mark style="color:purple;">loyalty gages</mark>_](../../../products-services/gages/loyalty-gage/)_<mark style="color:purple;">.</mark>_&#x20;

<mark style="color:purple;">At the time of the Initial Release V0, the Eternal Factory only deploys Loyalty Gage contracts. Loyalty Gages must implement an activating procedure,</mark> <mark style="color:purple;"></mark><mark style="color:purple;">`initialize`</mark><mark style="color:purple;">, on top of the gage's standard requirements of a closing procedure,</mark> <mark style="color:purple;"></mark><mark style="color:purple;">`exit`</mark><mark style="color:purple;">.</mark>&#x20;

## Functions

### viewTarget

```
function viewTarget() public view returns (uint256)
```

Depending on whether the loyalty gage's asset of reference is inflationary or deflationary, computes the target supply plus/minus the percent change condition for the total token supply of the asset.&#x20;

* `return: uint256` The minimum target supply which meets the percent change condition

### initialize

```
function initialize(address rAsset, address dAsset, uint256 rAmount, uint256 dAmount, uint256 rRisk, uint256 dRisk) external
```

Initializes a loyalty gage for a given receiver and distributor. Only callable by an Eternal contract.

* `rAsset`: The address of the asset deposited by the receiver
* `dAsset`: The address of the asset deposited by the distributor
* `rAmount`: The amount of the asset deposited by the receiver
* `dAmount`: The amount of the asset deposited by the distributor
* `rRisk`: The risk percentage of the receiver
* `dRisk`: The risk percentage of the distributor

### exit

```
function exit() external 
```

Closes the loyalty gage and determines the winner. Only callable by the receiver.&#x20;
