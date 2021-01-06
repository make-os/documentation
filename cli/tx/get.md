---
id: get
title: Get Transaction
sidebar_label: get
---

# get

The `get` command allows you to get a transaction object or status by its hash. Returns an object containing the `data` and the `status`. If `-s` flag is set, only the status of the transaction is printed out.

#### Status

* `In Mempool` - Indicates that the transaction is in the mempool.
* `In Pushpool` - Indicates that the transaction is in the push pool.
* `Confirmed` - Indicates that the transaction has been added into a confirmed block.

### Usage

```text
kit tx get [options] 
```

```text
Usage:
  kit tx get [flags] <hash>

Flags:
  -h, --help     help for get
  -s, --status   Show only status information
```

### Arguments

* `hash` - The transaction hash.

### Options

* `-s, --status` - Print out the status of the transaction only.
* `-h, --help` - Prints out a help message.

### Example

* Get a transaction by its hash.

{% tabs %}
{% tab title="Bash" %}
```bash
kit tx get 0x35d72037bea40cc824afa28dd145f954d6437f0c2ceb722b3faa6c7df9a62d29
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
  "data": {
    "delegate": null,
    "fee": "1",
    "nonce": 3,
    "senderPubKey": [67,155,203,212,6,5,51,24,234,106,169,130,184,236,235,83,105,122,64,91,11,54,228,7,143,69,81,88,62,96,19,203],
    "sig": [17,51,87,105,131,147,178,162,236,129,197,33,231,138,113,244,122,113,186,51,157,72,46,40,126,73,133,18,169,42,54,114,74,217,190,119,101,23,137,231,199,129,106,251,131,155,72,1,15,82,120,215,163,84,184,217,31,40,57,76,85,224,183,14],
    "timestamp": 1597921959,
    "type": 3,
    "value": "100"
  },
  "status": "in_mempool"
}
```
{% endtab %}
{% endtabs %}

* Get only the status of a transaction

{% tabs %}
{% tab title="Bash" %}
```bash
kit tx get 0x35d72037bea40cc824afa28dd145f954d6437f0c2ceb722b3faa6c7df9a62d29 --status
```
{% endtab %}

{% tab title="Output" %}
```
Status: In Mempool
```
{% endtab %}
{% endtabs %}

