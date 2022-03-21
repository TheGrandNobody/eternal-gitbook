---
description: The blueprint for all gages
---

# Gage

## <mark style="color:blue;">Introduction</mark>

_<mark style="color:purple;">The Gage.sol contract is an abstract contract serving as the standard list of requirements for any given contract to be defined as a</mark>_ [_<mark style="color:purple;">gage</mark>_](../../../products-services/gages/)_<mark style="color:purple;">.</mark>_&#x20;

<mark style="color:purple;">As all gages either inherit or implement the functions defined by the Gage contract, this maintains consistency of interaction with the Eternal Treasury. Note that the Eternal Factory does not deploy Gages, but rather,</mark> [<mark style="color:purple;">Loyalty Gage</mark>](loyalty-gage.md) <mark style="color:purple;">contracts.</mark>

## Enums

### Status

```
enum Status {
    Pending,
    Active,
    Closed
}
```

Any given gage has three different possible statuses: Pending, Active and Closed:&#x20;

1. A **Pending** gage is one which has been deployed but not initialized to completion, meaning some of its parameters may still be modified. For instance, take a gage which requires four stakeholders to join it before it becomes Active. If such a gage only contains two users and still requires two more, it would not be fully initialized. Hence,  the gage would have a Pending status.&#x20;
2. An **Active** gage is one which is fully initialized and cannot be modified any further (i.e, you cannot join an Active gage).&#x20;
3. A **Closed** gage is one for which the closing procedure, `exit`, has been called.&#x20;

## Functions

### viewGageUserCount

```
function viewGageUserCount() external view returns (uint256)
```

Returns the current number of users in this gage.

* `return: uint256` The number of users remaining in the gage

### viewCapacity

```
function viewCapacity() external view returns (uint256)
```

Returns the maximum number of users able to enter this gage.

* `return: uint256` The maximum number of users able to join this gage

### viewStatus

```
function viewStatus() external view returns (uint256)
```

Returns the status of the gage, where 0 corresponds to Pending, 1 to Active and 2 to Closed.

* `return: uint256` The current status of this gage

### viewLoyalty

```
function viewLoyalty() external view returns (bool)
```

Returns whether this gage falls under the loyalty gage category or not.

* `return: boolean` True if the gage is a loyalty gage, otherwise false

### viewUserData

```
function viewUserData(address user) external view returns (address, uint256, uint256)
```

View a given user's data for this gage.

* `user`: The address of the specified user
* `return: address` The address of the user's deposited asset in this gage
* `return: uint256` The amount of the user's deposited asset in this gage
* `return: uint256` The risk percentage of the user in this gage

## Events

### GageInitiated

```
event GageInitiated(uint256 id)
```

Signals the transition from a Pending status to an Active status for a gage with a unique id.

### GageClosed

```
event GageClosed(uint256 id, address indexed winner)
```

Signals the transition from an Active status to a Closed status for a gage with unique id and an address who the gage closed in favor of.&#x20;
