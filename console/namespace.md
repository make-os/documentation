---
id: namespace
title: Namespace Module
sidebar_label: Namespace
---

# namespace

This module allows you to create and manage namespaces. It can be accessed from the global variable `ns`.

## register

```javascript
ns.register(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Send a transaction to register a public key as a push key.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `name` - `String`: The unique name 
   * `value` - `String`: The namespace registration fee.
   * `to` - `String`: \(optional\) The user address or repository that will own and control the namespace.
   * `domains` - `Object`: The namespace domain and target pairs. The domain must contain only alphanumeric \(plus underscore and hyphen\) characters. The target must be a user address prefixed with `a/` or a repository name prefixed with `r/`.
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

* Create a transaction to register a namespace.

```javascript
ns.register({ 
   value: "1", 
   fee: "1", 
   name: "myname", 
   domains: {
      "target": "r/repo", 
      "target2": "a/os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u"
   },
}, user.getKey(accounts[0]))
```

## updateDomain

```javascript
ns.updateDomain(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Send a transaction to register a public key as a push key.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `name` - `String`: The unique name 
   * `domains` - `Object`: The namespace domain and target pairs. Domain must contain only alphanumeric \(plus underscore and hyphen\) characters. Target must be a user address prefixed with `a/` or a repository name prefixed with `r/`.
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

* Create a transaction to update the domains of a namespace.

```javascript
ns.updateDomain({ 
   value: "1", 
   fee: "1", 
   name: "ns-xyz", 
   domains: {
      "target": "r/repo"
   }
}, user.getKey(accounts[0]))
```

## lookup

```javascript
ns.lookup(name, [height])
```

Find a namespace by its name.

### Parameters

1. `name` - `String`: The name of the namespace.
2. `height` - `String|Number`: \(optional\) The block height to query \(Default: latest\).

### Returns

`Object` - **The result object**

* `name` - `String`: The namespace name.
* `owner` - `String`: The user address or repository that owns the namespace.
* `expiresAt` - `String`: The block height when the namespace lease expires.
* `graceEndAt` - `String`: The block height when grace period will end. 
* `expired` - `Boolean`: When true, it means the namespace has expired.
* `grace` - `Boolean`: When true, it means that namespace has expired and in the grace period.

### Example

* Create a transaction to register a namespace.

```javascript
ns.register({ 
   value: "1", 
   fee: "1", 
   name: "google", 
   domains: {
      "target": "r/repo", 
      "target2": "a/os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u"
   }
}, user.getKey(accounts[0]))
```

## getTarget

```javascript
ns.getTarget(path, [height])
```

Find a namespace by its name.

### Parameters

1. `path` - `String`: The domain path `namespace/domain`
2. `height` - `String|Number`: \(optional\) The block height to query \(Default: latest\).

### Returns

`String` - The target value

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// sends a transaction to register a namespace
ns.getTarget("myname/target")
```
{% endtab %}

{% tab title="Output" %}
```javascript
"r/repo"
```
{% endtab %}
{% endtabs %}

