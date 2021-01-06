---
id: ticket
title: Ticket Module
sidebar_label: Ticket
---

# ticket

This module allows you to purchase validator and host tickets that allow you to participate in network consensus operations. Ticket purchasing functions can be accessed from the global variable named `ticket`.

## buy

```javascript
ticket.buy(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Send a transaction to purchase a validator ticket.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `value` - `String`:  The amount of coins to pay for the ticket.
   * `delegate` - `String` : Delegate the ticket to another validator by providing their base58 encoded public key.
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

* Create a transaction to purchase a ticket worth 1000 units.

```javascript
ticket.buy({ 
   value: "1000",
   fee: "1"
}, user.getValidator(true).privateKey)
```

## host.buy

```javascript
ticket.host.buy(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Send a transaction to purchase a host ticket.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `value` - `String`:  The amount of coins to pay for the ticket.
   * `delegate` - `String` : Delegate the ticket to another host by providing their base58 encoded public key.
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

* Create a transaction to purchase a host ticket for 1000 coins. 

```javascript
ticket.host.buy({ 
   value: "1000",
   fee: "1"
}, user.getValidator(true).privateKey)
```

## list

```javascript
ticket.list(proposer, [queryopts])
```

Get validator tickets belonging to a proposer.

### Parameters

1. `proposer` - `String`: The base58 encoded public key of the proposer.
2. `queryopts` - `Object`: The query options
   * `expired` - `Boolean`: When true, only decayed tickets will be returned.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
ticket.list("48J1NrCGHu4D8qkbsGYKRRaVhJgPt3gfFmgwmSeNjMcrsX1fuas")
```
{% endtab %}

{% tab title="Output" %}
```javascript
[
  {
    "commissionRate": 35,
    "delegator": "",
    "expireBy": 14040,
    "hash": "0x126f53d2f957646b21d8d631198753775f87d6e8ad13cdf17f9338507eb734cc",
    "height": 22,
    "index": 1,
    "matureBy": 25,
    "proposerPubKey": [67,155,203,212,6,5,51,24,234,106,169,130,184,236,235,83,105,122,64,91,11,54,228,7,143,69,81,88,62,96,19,203],
    "type": 2,
    "value": "100"
  }
]
```
{% endtab %}
{% endtabs %}

## host.list

```javascript
ticket.host.list(proposer, [queryopts])
```

Get validator tickets belonging to a proposer.

### Parameters

1. `proposer` - `String`: The base58 encoded public key of the proposer.
2. `queryopts` - `Object`: The query options

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
ticket.host.list("48J1NrCGHu4D8qkbsGYKRRaVhJgPt3gfFmgwmSeNjMcrsX1fuas")
```
{% endtab %}

{% tab title="Output" %}
```javascript
[
  {
    "commissionRate": 35,
    "delegator": "",
    "expireBy": 14040,
    "hash": "0x126f53d2f957646b21d8d631198753775f87d6e8ad13cdf17f9338507eb734cc",
    "height": 22,
    "index": 1,
    "matureBy": 25,
    "proposerPubKey": [67,155,203,212,6,5,51,24,234,106,169,130,184,236,235,83,105,122,64,91,11,54,228,7,143,69,81,88,62,96,19,203],
    "type": 3,
    "value": "100"
  }
]
```
{% endtab %}
{% endtabs %}

