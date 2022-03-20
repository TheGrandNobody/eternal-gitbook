---
description: The treasury of the Eternal ecosystem, holding all of its value
---

# Eternal Treasury V0

## <mark style="color:blue;">Introduction</mark>

_<mark style="color:purple;">The EternalTreasury.sol contract is responsible for all financial operations in the Eternal ecosystem.</mark>_ <mark style="color:purple;"></mark><mark style="color:purple;"></mark>&#x20;

<mark style="color:purple;">This contract is ownable and owned by the Eternal Fund. The Eternal Treasury initiates gage contracts after they have been deployed by the Eternal Factory contract, taking care of any interaction with external contracts not pertaining to the Eternal ecosystem. Once a user exits a gage, the treasury also settles gage contracts by partitioning gage fees amongst stakers and buying back ETRNL using a percentage of the gaging fees that is proportional to the fee constant it holds.  As such, the treasury also provides</mark> [<mark style="color:purple;">active staking</mark>](../../../token/tokenomics/staking.md#active-staking) <mark style="color:purple;">services. It keeps track of all stakers' fees and modifies their staking/reserve balances using a similar technique to a cash-reserve ratio, in this case named the staking-reserve ratio. Last, the treasury carries all automatic liquidity provision operations whilst holding all of Eternal ecosystem's reserves, representative of its intrinsic value.</mark>

## Modifiers

### haltsActivity

```
modifier haltsActivity() {
    undergoingSwap = true;
    _;
    undergoingSwap = false;
}
```

Ensures the contract doesn't affect its AVAX balance when swapping ETRNL for AVAX during an automatic liquidity provision event. This also prevents it from getting caught in a circular liquidity event (swapping tokens when it was already swapping tokens).&#x20;

### activityHalted

```
modifier activityHalted() {
    require(!undergoingSwap, "A liquidity swap is in progress");
    _;
}
```

Prevents a given function from being used if an automatic liquidity provision event is occurring. Functions will revert if activity is halted (a liquidity swap is in progress). This modifier is used in conjunction with `haltsActivity`.&#x20;

## Functions

### initialize

```
function initialize(address _fund) external onlyAdmin
```

Initializes staking balances, the fee rate, fee constant and attributes "fund rights" to the Timelock contract. Only callable by the temporary admin.

### viewPair

```
function viewPair() external view returns (address)
```

Returns the address of the ETRNL/AVAX pair on Trader Joe.

* `return: address` The address of the ETRNL/AVAX pair

### viewUndergoingSwap

```
function viewUndergoingSwap() external view returns (bool)
```

Returns whether a liquidity swap is in progress or not. This is mainly used by the Eternal Factory to contract to ensures that a gage will be deployed successfully.

* `return: boolean` True if a liquidity swap is in progress, false otherwise

### convertToReserve

```
function convertToReserve(uint256 amount) public view returns (uint256)
```

Converts a given staked amount to the reserve number space.&#x20;

* `amount`: The specified staked amount
* `return: uint256` The staked amount in terms of its reserve number space

### convertToStaked

```
function convertToStaked(uint256 reserveAmount) public view returns (uint256)
```

Converts a given reserve amount to the regular (staked) number space.

* `reserveAmount`: The specified reserve amount
* `return: uint256`: The reserve amount in terms of the staked number space

### computeMinAmounts

```
function computeMinAmounts(address asset, address otherAsset, uint256 amountAsset, uint256 uncertainty) public view returns (uint256 minOtherAsset, uint256 minAsset, uint256 amountOtherAsset)
```

Computes the equivalent of an asset to an other asset and the minimum amount of the two needed to provide liquidity.

* `asset`: The first specified asset, whose amount is to be converted to the other asset
* `otherAsset`: The other specified asset
* `amountAsset`: The amount of the first specified asset
* `uncertainty`: The minimum loss to deduct from each minimum amount in case of price fluctuations
* `return: uint256` The minimum amount of otherAsset needed to provide liquidity (not given if uncertainty = 0)
* `return: uint256` The minimum amount of Asset needed to provide liquidity (not given if uncertainty = 0)
* `return: uint256` The equivalent in otherAsset of the given amount of asset

### updateReserves

```
function updateReserves(address user, uint256 amount, uint256 reserveAmount, bool add) public
```

Adds or subtracts a given amount from the treasury's reserves for a given user. Only callable by an Eternal contract.

* `user`: The address of the specified user
* `amount`: The specified amount of ETRNL being added/subtracted to/from the reserves
* `reserveAmount`: The reserve amount of ETRNL being added/subtracted to/from the reserves
* `add`: Whether the amount is to be added or subtracted to the reserves

### fundEternalLiquidGage

```
function fundEternalLiquidGage(address gage, address receiver, address asset, uint256 userAmount, uint256 rRisk, uint256 dRisk) external payable
```

Funds a given liquidity gage with ETRNL, provides liquidity using ETRNL and the receiver's asset and transfers a bonus to the receiver. Only callable by the Eternal Factory.

* `gage`: The address of the specified liquid gage
* `receiver`: The address of the receiver
* `asset`: The address of the asset being deposited by the receiver
* `userAmount`: The amount of the asset being deposited by the receiver
* `rRisk`: The receiver's risk percentage
* `dRisk`: The treasury's (distributor) risk percentage

### settleGage

```
function settleGage(address receiver, uint256 id, bool winner) external activityHalted
```

Settles a given ETRNL gage. Only callable by an Eternal-deployed gage.&#x20;

* `receiver`: The address of the receiver for this gage
* `id`: The unique id of the specified gage
* `winner`: Whether the gage closed in favor of the user or not

### stake

```
function stake(uint256 amount) external
```

Stakes a given amount of ETRNL into the treasury.

* `amount`: The specified amount of ETRNL being staked

### unstake

```
function unstake(uint256 amount) external override
```

Unstakes a user's given amount of ETRNL and transfers the user's accumulated rewards proportional to that amount (in ETRNL).

* `amount`: The specified amount of ETRNL being unstaked

### provideLiquidity

```
function provideLiquidity(uint256 contractBalance) external activityHalted
```

Provides liquidity to the ETRNL/AVAX pair on Trader Joe for the Eternal Token contract. Only callable by the Eternal Token contract.

* `contractBalance`:  The Eternal Token's contract's ETRNL balance that was transferred to the treasury

### withdrawAVAX

```
function withdrawAVAX(address recipient, uint256 amount) external onlyFund activityHalted
```

Transfers a given amount of AVAX from the contract to an address. Only callable by governance.

* `recipient`: The address to which the AVAX is to be sent
* `amount`: The specified amount of AVAX to transfer

### withdrawAsset

```
function withdrawAsset(address asset, address recipient, uint256 amount) external onlyFund
```

Transfers a given amount of a token from the contract to an address. Only callable by governance.

* `asset`: The address of the asset being withdrawn
* `recipient`: The address to which the asset is to be sent
* `amount`: The specified amount of asset to transfer

### setEternalFactory

```
function setEternalTreasury(address newContract) external onlyFund
```

Updates the address of the Eternal Factory contract. Only callable by governance.

* `newContract`: The address of the new Eternal Factory

### setEternalToken

```
function setEternalToken (address newContract) external onlyFund
```

Updates the address of the Eternal Token contract. Only callable by governance.

* `newContract`: The address of the new Eternal Token

## Events

### AVAXTransferred

```
event AVAXTransferred(uint256 amount, address recipient)
```

Signals that part of the locked AVAX balance has been cleared to a given address by decision of governance.

### AssetTransferred

```
event AssetTransferred(address asset, uint256 amount, address recipient)
```

Signals that some of an asset balance has been sent to a given address by decision of governance.
