---
id: pushkey
title: Push Key Module
sidebar_label: Push Key
---

# pushkey

This module allows you to create and manage push keys. It can be accessed from the global variable `pk`.

## register

```javascript
pk.register(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Send a transaction to register a public key as a push key.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `pubKey` - `String`:  \(optional\) A base58 encoded public key to be registered.
   * `scopes` - `Array<String>`: \(optional\) A list of repositories or namespaces where the push key can be used.
   * `feeCap` - `String`: \(optional\) The maximum amount of fee the key can spend from its creator's account. 
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The unix timestamp of the transaction.
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key that will be used to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.
* `address` - `String`: A bech32 encoded push key address.

### Example

* Create a transaction to register a public key on the network.

```javascript
pk.register({ 
   pubKey: "49G1iGk8fY7RQcJQ7LfQdThdyfaN8dKfxhGQSh8uuNaK35CgazZ",
   fee: 1
}, user.getKey(accounts[0]))
```

## update

```javascript
pk.update(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Send a transaction to update a previously registered public key.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `id` - `String`: The push key address.
   * `addScopes` - `Array<String>`:  \(optional\) A list of repositories or namespaces where the push key can be used.
   * `removeScopes` - `Array<Number>`: \(optional\) Index of scopes to be removed.
   * `feeCap` - `String`: \(optional\) The maximum amount of fee the key can spend from its creator's account. 
   * `delete` - `Boolean`: Indicates that the public key should be deleted.
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

* Create a transaction to update a push key.

```javascript
pk.update({
   id:"pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7", 
   addScopes:"repos/", 
   removeScopes:[0], 
   fee: "0.01"
}, user.getKey(accounts[0]))
```

## unregister

```javascript
pk.unregister(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Send a transaction to delete a public key.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `id` - `String`: The push key address.
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

* Create a transaction to unregister a push key from the network.

```javascript
pk.unregister({
   id:"pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7",  
   fee: "0.01"
}, user.getKey(accounts[0]))
```

## get

```javascript
pk.get(address, [height])
```

Get a push key by its address.

### Parameters

1. `address` - `String`: The push key address.
2. `height` - `Number|String`: \(optional\) The block height to query \(Default: latest\). 

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
pk.get("pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7")
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
  "address": "os1wfx7vp8qfyv98cctvamqwec5xjrj48tpklxklh",
  "feeCap": "0",
  "feeUsed": "0",
  "pubKey": [194,198,203,80,111,17,78,208,207,230,2,194,128,230,32,142,235,100,71,14,125,69,42,169,244,21,135,16,221,231,27,230]
}
```
{% endtab %}
{% endtabs %}

## getByAddress

```javascript
pk.getByAddress(address)
```

Get a list of push keys belonging to an address.

### Parameters

1. `address` - `String`: The push key address.

### Returns

`Array<Object>` - **The list of objects**

* `address` - `String`: The address of the push key owner.
* `feeCap` - `String`: The maximum fee the push key is allowed to spend from the owner’s account.
* `feeUsed` - `String`: The amount of Latinum spent on fees. 
* `pubKey` -  `Array<Number>` - The public key 

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
pk.get("pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7")
```
{% endtab %}

{% tab title="" %}
```javascript
{
  "address": "os1wfx7vp8qfyv98cctvamqwec5xjrj48tpklxklh",
  "feeCap": "0",
  "feeUsed": "0",
  "pubKey": [194,198,203,80,111,17,78,208,207,230,2,194,128,230,32,142,235,100,71,14,125,69,42,169,244,21,135,16,221,231,27,230]
}
```
{% endtab %}
{% endtabs %}

## getAccountOfOwner

```javascript
pk.getOwner(address, [height])
```

Get the account that owns the given push key.

### Parameters

1. `address` - `String`: The push key address.
2. `height` - `Number|String`: \(optional\) The block height to query \(Default: latest\). 

### Returns

Account

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
pk.getOwner("pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7")
```
{% endtab %}

{% tab title="Output" %}
```javascript
{ 
   "balance": "4979.98",
   "nonce": "19",
}
```
{% endtab %}
{% endtabs %}

