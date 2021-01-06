---
id: user
title: User Module
sidebar_label: User
---

# user

This module allows you to access both personal information of the node runner. The module is accessed from the global variable `user`.

## getKeys

```javascript
user.getKeys()
```

Gets the address of all keys stored on the keystore of the node.

### Returns

`Array<String>`: A list of addresses.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
user.getKeys()
```
{% endtab %}

{% tab title="Output" %}
```javascript
[
   "os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u",
   "os1wfx7vp8qfyv98cctvamqwec5xjrj48tpklxklh"
]
```
{% endtab %}
{% endtabs %}

## getKey

```javascript
user.getKey(addrOrIndex, [passphrase])
```

Gets the private key of a key by its address or keystore index. If the key exists, it will be unlocked using the provided `passphrase`. If `passphrase` is not provided, an interactive prompt will be launched to ask for it.

### Parameters

1. `addrOrIndex` - `String|Number`: The address or keystore index of the key
2. `passphrase` - `String`: \(Optional\) The passphrase to use to unlock the key. If not provided, you will be prompted to provide it. 

### Returns

`String`: The base58 encoded private key.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
user.getKey("os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u")
```
{% endtab %}

{% tab title="Output" %}
```javascript
"wXVFmgEmKumxVnQGSnL67krnWkBj4Q...W711b7UnmARiUWtSNSJ6pVhmk1ppiPQPGrD8F3"
```
{% endtab %}
{% endtabs %}

## getPublicKey

```javascript
user.getPublicKey(addrOrIndex, [passphrase])
```

Gets the public key of a key by its address or keystore index. If the key exists, it will be unlocked using the provided `passphrase`. If `passphrase` is not provided, an interactive prompt will be launched to ask for it.

### Parameters

1. `addrOrIndex` - `String|Number`: The address or keystore index of the key
2. `passphrase` - `String`: \(Optional\) The passphrase to use to unlock the key. If not provided, you will be prompted to provide it. 

### Returns

`String`: The base58 encoded public key.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
chain.getPublicKey("os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u")
```
{% endtab %}

{% tab title="Output" %}
```javascript
"48hpSpVR39MX947pHPSxRzKHoe65rLWzLWuC14sBU1n6tu7Jg5x"
```
{% endtab %}
{% endtabs %}

## getNonce

```javascript
user.getNonce(address, [height])
```

Gets the current nonce of a user account.

### Parameters

1. `address` - `String`: The address of the target user account.
2. `height` - `String|Number`: \(Optional\) The block height to query \(Default: latest\).

### Returns

`String`: The current nonce.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
user.getNonce("os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u")
```
{% endtab %}

{% tab title="Output" %}
```javascript
"12"
```
{% endtab %}
{% endtabs %}

## get

```javascript
user.get(address, [height])
```

Gets a user account by its address.

### Parameters

1. `address` - `String`: The address of the target user account.
2. `height` - `String|Number`: \(Optional\) The block height to query \(Default: latest\).

### Returns

`Object`: **The account object** `balance` - `String`: The native coin balance. `nonce` - `String`: The account nonce. `stakes` - `Object`: Staked coin information `delegatorCommission` - `String`: Commission to receive from delegators.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
user.get("os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u")
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
  "balance": "1984872.35",
  "nonce": "91"
}
```
{% endtab %}
{% endtabs %}

## getBalance

```javascript
user.getBalance(address, [height])
```

Gets the coin balance of a user account.

### Parameters

1. `address` - `String`: The address of the target user account.
2. `height` - `String|Number`: \(Optional\) The block height to query \(Default: latest\).

### Returns

`String`: The coin balance.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
user.getBalance("os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u")
```
{% endtab %}

{% tab title="Output" %}
```javascript
"12.3"
```
{% endtab %}
{% endtabs %}

## getStakedBalance

```javascript
user.getStakedBalance(address, [height])
```

Gets the total amount of the native coin a user account has staked.

### Parameters

1. `address` - `String`: The address of the target user account.
2. `height` - `String|Number`: \(Optional\) The block height to query \(Default: latest\).

### Returns

`String`: The coin balance.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
user.getStakedBalance("os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u")
```
{% endtab %}

{% tab title="Output" %}
```javascript
"12.3"
```
{% endtab %}
{% endtabs %}

## getValidator

```javascript
user.getValidator(includePrivKey)
```

Gets the node’s validator key.

### Parameters

1. `includePrivKey` - `Boolean`: When true, the private key is included in the result.

### Returns

`Object`: The validator key information.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
user.getValidator(true)
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
    "address": "os174vnayvd6teyzcfze5z7xsdmzg4kxk8l6jry7n",
    "privateKey": "wnrZynYB6837qB5mRN7V4To1MDB...nYZxaU9qQZPWhsFUPHefAdQEyRUu",
    "publicKey": "48J1NrCGHu4D8qkbsGYKRRaVhJgPt3gfFmgwmSeNjMcrsX1fuas",
    "tmAddress": "5CFFB08E0403EF88770EBAEA3499324779D0FB06"
}
```
{% endtab %}
{% endtabs %}

## setCommission

```javascript
user.setCommission(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Create a transaction that updates the delegator commission percentage of a validator account.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `commission` - `String`:  The percentage of reward to receive from delegators.
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The unix timestamp of the transaction.
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key to use to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

```javascript
user.setCommission({ 
    commission: "100",
    fee: "1"
}, user.getKey(accounts[0]))
```

## send

```javascript
user.send(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Create a transaction that sends coins from the signers account to another account or repository.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `value` - `Number|String`:  The amount of native coin to be sent.
   * `to` - `String`: The address of the recipient; A user address or a repository name prefixed with `r/`.
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The unix timestamp of the transaction.
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key to use to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

```javascript
user.send({ 
    to: "os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u", 
    value:"5000", 
    fee: "1" 
}, user.getKey(accounts[0]))
```

