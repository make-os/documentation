---
id: transaction
title: Transaction Module
sidebar_label: Transaction
---

# transaction

This module provides methods for fetching transactions and sending signed transaction payload. The module is accessed from the global variable `tx`.

## get

```javascript
tx.get(hash)
```

Gets the address of all keys stored on the keystore of the node.

### Parameters

1. `hash` - `String`: The transaction hash

### Returns

`Object`: **The result object** `data` - `Object`: The transaction object. `status` - `String`: The status of the transaction.

* `in_mempool` means the transaction is in the mempool.
* `in_pushpool` means the transaction is in the pushpool
* `in_block` means the transaction has been processed.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
tx.get("0x23a7f9a8cb6c38703b1b77da09081733f3a36a67b5a0df104f190e21dd3486b2")
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
  "data": {
    "fee": "1",
    "nonce": 92,
    "senderPubKey": [121,172,241,123,81,102,72,134,112,163,3,245,128,196,144,219,42,147,70,184,226,63,26,28,135,151,128,139,16,82,174,4],
    "sig": [235,196,116,213,16,136,10,226,235,149,32,92,110,34,165,150,153,218,68,75,105,234,98,156,70,47,54,93,118,131,19,230,44,176,20,96,164,116,10,223,58,29,236,227,118,91,32,161,60,20,203,204,117,124,195,177,189,198,36,122,2,29,56,12],
    "timestamp": 1597695235,
    "type": 3,
     ... other transaction type-specific fields
  },
  "status": "in_block"
}
```
{% endtab %}
{% endtabs %}

## send

```javascript
tx.send(payload)
```

Send a signed transaction payload to the network.

### Parameters

1. `payload` - `Object`: The transaction payload

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

```javascript
tx.send({
  "fee": "1",
  "nonce": 93,
  "senderPubKey": [121,172,241,123,81,102,72,134,112,163,3,245,128,196,144,219,42,147,70,184,226,63,26,28,135,151,128,139,16,82,174,4],
  "sig": [204,75,69,60,13,109,229,180,140,112,242,46,67,157,49,124,25,77,61,38,246,95,120,241,235,137,96,117,165,169,34,174,234,152,109,216,63,0,130,146,34,94,114,205,9,214,150,165,41,28,111,235,148,19,13,1,221,137,63,109,247,73,97,1],
  "timestamp": 1597696366,
  "type": 3
})
```

