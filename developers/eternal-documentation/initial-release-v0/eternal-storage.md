---
description: The shared eternal storage for all Eternal smart contracts
---

# Eternal Storage

## <mark style="color:blue;">Introduction</mark>

_<mark style="color:purple;">The EternalStorage.sol contract holds all variables of all other Eternal smart contracts by implementing an</mark>_ [_<mark style="color:purple;">eternal storage pattern</mark>_](https://fravoll.github.io/solidity-patterns/eternal\_storage.html)_<mark style="color:purple;">.</mark>_&#x20;

<mark style="color:purple;">In this implementation of the Eternal Storage, single variables and mappings can be contract-specific (i.e, two contracts can have variables with identical names). However, this is not the case for array variables due to the overall lack of arrays being used in the Initial Release V0 contracts. Furthermore, the Eternal Storage is designed to never be replaced or redeployed again. Hence, it contains any possible types which could be used in future Eternal smart contracts but does not necessarily use at present.</mark>

## Modifiers

### onlyLatestVersion

```
modifier onlyLatestVersion() {
     bytes32 entity = keccak256(abi.encodePacked(_msgSender()));
     require(_msgSender() == addresses[eternalStorage][entity], "Old contract can't edit storage");
     _;
}
```

Ensures that contracts can only modify the storage if the keccak-256 hash of their address is stored in the storage. This is mainly used to prevent older contracts from accessing storage. Note that this does not prevent any given address from viewing the storage's contents.

## Functions

### initialize

```
function initialize(address _token, address _factory, address _treasury, address _offering, address _timelock, address _fund) external 
```

Initializes the storage by storing the keccak-256 hashes of each Eternal smart contract's address.

* `_token`: The address of the initial EternalToken.sol contract
* `_factory`: The address of the initial EternalFactory.sol contract
* `_treasury`: The address of the initial EternalTreasury.sol contract
* `_offering`: The address of the EternalOffering.sol contract
* `_timelock`: The address of the Timelock.sol contract
* `_fund`: The address of the EternalFund.sol contract

### setUint

```
function setUint(bytes32 entity, bytes32 key, uint256 value) external onlyLatestVersion
```

Stores a uint256 value for a given contract and key.

* `entity`: The keccak-256 hash of the contract's address
* `key`:The specified mapping key
* `value`: The specified uint256 value

### setInt

```
function setInt(bytes32 entity, bytes32 key, int256 value) external onlyLatestVersion
```

Stores an int256 value for a given contract and key.

* `entity`: The keccak-256 hash of the contract's address
* `key`:The specified mapping key
* `value`: The specified int256 value

### setAddress

```
function setAddress(bytes32 entity, bytes32 key, address value) external onlyLatestVersion
```

Stores an address value for a given contract and key.

* `entity`: The keccak-256 hash of the contract's address
* `key`:The specified mapping key
* `value`: The specified address value

### setBool

```
function setBool(bytes32 entity, bytes32 key, bool value) external override onlyLatestVersion
```

Stores a boolean value for a given contract and key.

* `entity`: The keccak-256 hash of the contract's address
* `key`:The specified mapping key
* `value`: The specified boolean value

### setBytes

```
function setBytes(bytes32 entity, bytes32 key, bytes32 value) external onlyLatestVersion
```

Stores a bytes32 value for a given contract and key.

* `entity`: The keccak-256 hash of the contract's address
* `key`:The specified mapping key
* `value`: The specified bytes32 value

### setUintArrayValue

```
function setUintArrayValue(bytes32 key, uint256 index, uint256 value) external onlyLatestVersion
```

Either stores a uint256 value to an array at a given index or pushes the value at the end of the array, for a given key.

* `key`:The specified mapping key
* `index`: The specified index of the array's element being modified (0 if pushing)
* `value`: The specified uint256 value

### setIntArrayValue

```
function setIntArrayValue(bytes32 key, uint256 index, int256 value) external onlyLatestVersion
```

Either stores an int256 value to an array at a given index or pushes the value at the end of the array, for a given key.

* `key`:The specified mapping key
* `index`: The specified index of the array's element being modified (0 if pushing)
* `value`: The specified int256 value

### setAddressArrayValue

```
function setAddressArrayValue(bytes32 key, uint256 index, address value) external onlyLatestVersion
```

Either stores an address value to an array at a given index or pushes the value at the end of the array, for a given key.

* `key`:The specified mapping key
* `index`: The specified index of the array's element being modified (0 if pushing)
* `value`: The specified address value

### setBoolArrayValue

```
function setBoolArrayValue(bytes32 key, uint256 index, bool value) external onlyLatestVersion
```

Either stores a boolean value to an array at a given index or pushes the value at the end of the array, for a given key.

* `key`:The specified mapping key
* `index`: The specified index of the array's element being modified (0 if pushing)
* `value`: The specified boolean value

### setBytesArrayValue

```
function setBytesArrayValue(bytes32 key, uint256 index, bytes32 value) external onlyLatestVersion
```

Either stores a bytes32 value to an array at a given index or pushes the value at the end of the array, for a given key.

* `key`:The specified mapping key
* `index`: The specified index of the array's element being modified (0 if pushing)
* `value`: The specified bytes32 value

### getUint

```
function getUint(bytes32 entity, bytes32 key) external view returns (uint256)
```

Returns a uint256 value for a given contract and key.

* `entity`:The keccak-256 hash of the specified contract's address
* `key`:The specified mapping key
* `return: uint256` The uint256 value mapped to the key for this entity

### getInt

```
function getInt(bytes32 entity, bytes32 key) external view returns (int256)
```

Returns an int256 value for a given contract and key.

* `entity`:The keccak-256 hash of the specified contract's address
* `key`:The specified mapping key
* `return: int256` The int256 value mapped to the key for this entity

### getAddress

```
function getAddress(bytes32 entity, bytes32 key) external view returns (address)
```

Returns an address value for a given contract and key.

* `entity`:The keccak-256 hash of the specified contract's address
* `key`:The specified mapping key
* `return: address` The address value mapped to the key for this entity

### getBool

```
function getBool(bytes32 entity, bytes32 key) external view returns (bool)
```

Returns a boolean value for a given contract and key.

* `entity`:The keccak-256 hash of the specified contract's address
* `key`:The specified mapping key
* `return: boolean` The boolean value mapped to the key for this entity

### getBytes

```
function getBytes(bytes32 entity, bytes32 key) external view returns (bytes32)
```

Returns a bytes32 value for a given contract and key.

* `entity`:The keccak-256 hash of the specified contract's address
* `key`:The specified mapping key
* `return: bytes32` The bytes32 value mapped to the key for this entity

### getUintArrayValue

```
function getUintArrayValue(bytes32 key, uint256 index) external view returns (uint256)
```

Returns a uint256 array's element's value for a given key and index.

* `key`: The specified mapping key
* `index`: The specified index of the desired value
* `return: uint256` The uint256 value at the specified index for the specified array

### getIntArrayValue

```
function getIntArrayValue(bytes32 key, uint256 index) external view returns (int256)
```

Returns an int256 array's element's value for a given key and index.

* `key`: The specified mapping key
* `index`: The specified index of the desired value
* `return: int256` The int256 value at the specified index for the specified array

### getAddressArrayValue

```
function getAddressArrayValue(bytes32 key, uint256 index) external view returns (address)
```

Returns an address array's element's value for a given key and index.

* `key`: The specified mapping key
* `index`: The specified index of the desired value
* `return: address` The address value at the specified index for the specified array

### getBoolArrayValue

```
function getBoolArrayValue(bytes32 key, uint256 index) external view returns (bool)
```

Returns a boolean array's element's value for a given key and index.

* `key`: The specified mapping key
* `index`: The specified index of the desired value
* `return: boolean` The boolean value at the specified index for the specified array

### getBytesArrayValue

```
function getBytesArrayValue(bytes32 key, uint256 index) external view returns (bytes32)
```

Returns a bytes32 array's element's value for a given key and index.

* `key`: The specified mapping key
* `index`: The specified index of the desired value
* `return: bytes32` The bytes32 value at the specified index for the specified array

### deleteUint

```
function deleteUint(bytes32 key, uint256 index) external onlyLatestVersion
```

Deletes a uint256 array's element for a given key and index

* `key`: The specified mapping key
* `index`: The specified index of the desired element

### deleteInt

```
function deleteInt(bytes32 key, uint256 index) external onlyLatestVersion
```

Deletes an int256 array's element for a given key and index

* `key`: The specified mapping key
* `index`: The specified index of the desired element

### deleteAddress

```
function deleteAddress(bytes32 key, uint256 index) external onlyLatestVersion
```

Deletes an address array's element for a given key and index

* `key`: The specified mapping key
* `index`: The specified index of the desired element

### deleteBool

```
function deleteBool(bytes32 key, uint256 index) external onlyLatestVersion
```

Deletes a boolean array's element for a given key and index

* `key`: The specified mapping key
* `index`: The specified index of the desired element

### deleteBytes

```
function deleteBytes(bytes32 key, uint256 index) external onlyLatestVersion
```

Deletes a bytes32 array's element for a given key and index

* `key`: The specified mapping key
* `index`: The specified index of the desired element

### lengthUint

```
function lengthUint(bytes32 key) external view returns (uint256)
```

Returns the length of a uint256 array for a given key.

* `key`: The specified mapping key
* `return: uint256` The length of the array mapped to the key

### lengthInt

```
function lengthInt(bytes32 key) external view returns (uint256)
```

Returns the length of an int256 array for a given key.

* `key`: The specified mapping key
* `return: uint256` The length of the array mapped to the key

### lengthAddress

```
function lengthAddress(bytes32 key) external view returns (uint256)
```

Returns the length of an address array for a given key.

* `key`: The specified mapping key
* `return: uint256` The length of the array mapped to the key

### lengthBool

```
function lengthBool(bytes32 key) external view returns (uint256)
```

Returns the length of a boolean array for a given key.

* `key`: The specified mapping key
* `return: uint256` The length of the array mapped to the key

### lengthBytes

```
function lengthBytes(bytes32 key) external view returns (uint256)
```

Returns the length of a bytes32 array for a given key.

* `key`: The specified mapping key
* `return: uint256` The length of the array mapped to the key
