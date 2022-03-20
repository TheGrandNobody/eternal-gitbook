---
description: The governance/utility token of the Eternal ecosystem
---

# Eternal Token V0

## <mark style="color:blue;">Introduction</mark>

_<mark style="color:purple;">The EternalToken.sol contract implements the functionality of</mark>_ [_<mark style="color:purple;">ETRNL</mark>_](../../../token/tokenomics/)_<mark style="color:purple;">, an ERC-20 compliant token used for both governance and maintaining sustainability in the Eternal ecosystem.</mark>_&#x20;

<mark style="color:purple;">The contract is</mark> [<mark style="color:purple;">ownable</mark>](ownable-enhanced.md)<mark style="color:purple;">, and is owned by the Eternal Fund. The Eternal Token contract implements fees on transactions  in the form of burning, automatic liquidity provision, funding and reward redistribution mechanisms, making the token a reflection token. Fees on transactions remove the necessity for a rebase mechanism and allow for a</mark> [<mark style="color:purple;">circular flow of ETRNL</mark>](../../../token/tokenomics/#circular-flow-of-etrnl)<mark style="color:purple;">. The contract also keeps track of the amount of ETRNL transacted daily that is subject to fees, periodically updating the</mark> [<mark style="color:purple;">Eternal Factory</mark> ](eternal-factory-v0.md)<mark style="color:purple;">contract with this data.</mark>

## Functions

## initialize

```
function initialize(address _factory, address _eternalTreasury, address _offering, address _timelock, address _fund, address _seedLock, address _privLock) external onlyAdmin
```

Initializes the tokens supplies, fee rates and the Treasury, Factory and Fund interfaces. Excludes Eternal contracts from rewards and/or fees. The caller of the function is also excluded from fees in order to allow him to provide initial liquidity for the token without it being subject to fees. The function finishes by giving "fund rights" to the Timelock contract. Only callable by the temporary admin.

* `_factory`: The address of the initial Eternal Factory contract
* `_eternalTreasury`: The address of the initial Eternal Treasury contract
* `_offering`: The address of the Eternal Offering contract
* `_timelock`: The address of the Timelock contract
* `_fund`: The address of the Eternal Fund contract
* `_seedLock`: The address of the FundLock contract used for seed sales
* `_privLock`:  The address of the FundLock contract used for private sales

### name

```
function name() external pure returns (string memory)
```

Returns the name of the token.

* `return: string` "Eternal Token"

### symbol

```
function symbol() external pure returns (string memory)
```

Returns the token ticker.

* `return: string` "ETRNL"

### decimals

```
function decimals() external pure returns (uint8)
```

Returns the number of decimals used by the token.

* `return: uint8` 18

### totalSupply

```
function totalSupply() external view returns (uint256)
```

Returns the current circulating supply of the Eternal token.

* `return: uint256` The total supply of the Eternal token

### balanceOf

```
function balanceOf(address account) public view returns (uint256)
```

Views the ETRNL balance of a given user address (account)

* `account`: The address of the specified account who we are viewing the balance of
* `return: uint256` The ETRNL balance of the specified address

### allowance

```
function allowance(address owner, address spender) external view returns (uint256)
```

Views the allowance of a given spender address for a given owner address.

* `owner`: The address of the specified owner
* `spender`: The address of the specified spender
* `return: uint256` The allowance of the spender for the owner

### getReflectionRate

```
function getReflectionRate() public view returns (uint256)
```

Computes the current rate used to inter-convert from the mathematically reflected space to the "true" or total space.

* `return: uint256` The ratio of the reflected total supply to the true total supply

### transfer

```
function transfer(address recipient, uint256 amount) external returns (bool)
```

Transfer a given amount to a given recipient address.

* `recipient`: The address of the specified recipient
* `amount`: The specified amount of ETRNL to transfer
* `return: boolean` True if the transfer is successful false otherwise

### approve

```
function approve(address spender, uint256 amount) external returns (bool)
```

Sets the allowance of a given spender to a given amount

* `spender`: The address of the specified spender
* `amount`: The specified amount the allowance of the spender is set to
* `return: boolean` True if the approval is successful, false otherwise

### transferFrom

```
function transferFrom(address sender, address recipient, uint256 amount) external returns (bool)
```

Transfer a given amount of ETRNL for a given sender address to a given recipient address. Updates allowances accordingly.&#x20;

* `sender`: The address of the specified sender
* `recipient`: The address of the specified recipient
* `amount`: The specified amount of ETRNL being transferred
* `return: boolean` True if the transfer is successful, false otherwise

### excludeFromReward

```
function excludeFromReward(address account) public onlyFund
```

Excludes a given address from receiving ETRNL token rewards. Only callable by governance. This does not work if the address is already excluded from rewards.&#x20;

* `account`: The specified address being excluded from rewards

### includeInReward

```
function includeInReward(address account) external onlyFund
```

Allows a given address to accrue rewards. Only callable by governance. This does not work if the address is already included in reward accrual.&#x20;

* `account`: The specified address being included in reward accrual

### setEternalTreasury

```
function setEternalTreasury(address newContract) external onlyFund
```

Updates the address of the Eternal Treasury contract. Only callable by governance.

* `newContract`: The address of the new Eternal Treasury

### setEternalFactory

```
function setEternalFactory (address newContract) external onlyFund
```

Updates the address of the Eternal Factory contract. Only callable by governance.

* `newContract`: The address of the new Eternal Factory

## Events

### Approval

```
event Approval(address indexed owner, address indexed spender, uint256 value)
```

Signals that the allowance of a spender for an owner was set to a new value by calling the `approve` function.

### Transfer

```
event Transfer(address indexed from, address indexed to, uint256 value)
```

Emitted when an amount (value) of tokens are moved from one address (from) to another (to) by calling the internal `_transfer` function.
