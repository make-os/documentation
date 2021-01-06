---
id: node
title: Node Module
sidebar_label: Node
---

# node

This module allows you to get information about the node and blockchain. It can be accessed from the global variable `node`.

## getBlock

```javascript
node.getBlock(height)
```

Get a tendermint block at the given height.

### Parameters

1. `height` - `String|Number`: The target block height

### Returns

[Tendermint Block](https://docs.tendermint.com/master/spec/core/data_structures.html#block)

### Example

```javascript
node.getBlock(101)
```

## getHeight

```javascript
node.getHeight()
```

Get the current height of the blockchain.

### Returns

`String` - The height of the node.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
node.getHeight()
```
{% endtab %}

{% tab title="Output" %}
```javascript
"123"
```
{% endtab %}
{% endtabs %}

## getBlockInfo

```javascript
node.getBlockInfo(height)
```

Get a summary block at the given height. This block information is indexed by MakeOS \(not Tendermint\).

### Parameters

1. `height` - `String|Number`: The target block height

### Returns

`String` - The height of the node.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
node.getBlockInfo(101)
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
    "appHash": "taKg/qP1ER5I4kI6Kw9es1aWNZtYklVh1WhhMJm5LLw=",
    "hash": "Id6OEYekHgLNiT7ZEGibbkVJZnMREgUUnRxWoLM1pPc=",
    "height": "101",
    "lastAppHash": "0dmLRT0oSfxQroggDk/2hnGDDGwU+CX4iH/nhPPX1i8=",
    "proposerAddress": "3PSYFHDDgGUTdOrG+1DY5aX92B4=",
    "time": "1597666979"
}
```
{% endtab %}
{% endtabs %}

## getValidators

```javascript
node.getValidators(height)
```

Get a list of validators that processed a given block.

### Parameters

1. `height` - `String|Number`: The target block height whose validators will be returned.

### Returns

`Object` - **The result object**

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
node.getValidators(101)
```
{% endtab %}

{% tab title="Output" %}
```javascript
[
    {
        "address": "os1858effdlfecl30hgq0dvpesygp2daf97malemz",
        "publicKey": "48gS3kCMVTJjHvJBwuQXXAFwYgJiATE7xJY34UuAJVbuHDoEZ2V",
        "ticketId": "0x",
        "tmAddress": "DCF4981470C380651374EAC6FB50D8E5A5FDD81E"
    }
]
```
{% endtab %}
{% endtabs %}

## isSyncing

```javascript
node.isSyncing()
```

Checks whether the node is currently synchronizing blocks and state with peers.

### Returns

`Boolean`

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
node.isSyncing()
```
{% endtab %}

{% tab title="Output" %}
```javascript
true
```
{% endtab %}
{% endtabs %}

