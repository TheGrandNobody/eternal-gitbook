---
description: A basic access control mechanism
---

# Ownable Enhanced

## <mark style="color:blue;">Introduction</mark>

<mark style="color:purple;">The OwnableEnhanced.sol contract is a modified version of</mark> [<mark style="color:purple;">Open Zeppelin's Ownable contract</mark>](https://docs.openzeppelin.com/contracts/4.x/api/access#Ownable)<mark style="color:purple;">.</mark>

<mark style="color:purple;">Aside from providing the same mechanics as Ownable.sol, OwnableEnhanced also introduces a temporary admin which loses his admin powers after 24 hours. This is used in allowing the temporary admin to initialize all other Eternal contracts before they become fully decentralized and governed by the Eternal Fund.</mark>&#x20;

## Modifiers

### onlyAdmin

```
modifier onlyAdmin() {
    require(admin() == _msgSender(), "Caller is not the admin");
    require(ownershipDeadline > block.timestamp, "Admin's rights are over");
    _;
}
```

Prevents any other accounts from using a function except for the designated temporary admin.

### onlyFund

```
modifier onlyFund() {
    require(_msgSender() == fund(), "Caller is not the fund");
    _;
}
```

Prevents any other accounts from using a function except for the Eternal Fund's associated Timelock contract.&#x20;

## Functions

### admin

```
function admin() public view returns (address)
```

Returns the address of the designated temporary admin.

* `return: address` The address of the temporary admin

### fund

```
function fund() public view returns (address)
```

Returns the address of the current governance.

* `return: address` The address of the current Timelock contract used by the Eternal Fund

### attributeFundRights

```
function attributeFundRights(address newFund) public onlyFund
```

Attributes the Eternal "fund rights" to a given address. Only callable by the current governance.

* `newFund`: The address of the new Timelock contract to give "fund rights" to

## Events

### FundRightsAttributed

```
event FundRightsAttributed(address indexed newFund)
```

Signals that a new contract has been designated as the Eternal Fund.
