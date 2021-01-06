---
id: send-fund
title: Send Funds
sidebar_label: Send Funds
description: Transfer coins between accounts and repositories.
---

# Send Coins

The native coin can be transferred from one account to another account by creating and sending a `TxCoinTransfer` transaction.

## Example

{% tabs %}
{% tab title="Console" %}
```javascript
user.send({ 
   to: "os1858effdlfecl30hgq0dvpesygp2daf97malemz", 
   value:"5000",
   fee: "1",
   nonce: 3,
}, user.getKey(accounts[0], "passphrase"))
```
{% endtab %}

{% tab title="CLI" %}
```bash
lob user send "os1858effdlfecl30hgq0dvpesygp2daf97malemz"  \
    --fee=1.2  \
    --value=5000  \
    --nonce=3  \
    --signing-key=0
```
{% endtab %}
{% endtabs %}

The code above calls the `user.send` console method, passing to it the transaction data and a key from the key store.

In the example above, we unlock Alice’s private key using `user.getKey`, set the transfer value to `5000` and fee to `1`.

`to` specifies the recipient of the transaction value. To can be a user address or a repository full address.

`nonce` is the number of all transactions Alice’s key has sent to the network. The nonce value is used to order Alice’s transactions and prevent a double-spend attack. If not provided, it will be automatically set.

{% hint style="info" %}
On the console, the `accounts`global variable contains a list of address of keys on the keystore.
{% endhint %}

### Send Coins to a Repository

```javascript
var alicePrivateKey = user.getKey(accounts[0], "passphrase")
user.send({ 
   to: "r/cashmap", 
   value:"5000",
   fee: "1",
   nonce: 3,
}, alicePrivateKey)
```

Here we are transferring `5000` coins to a repository called `cashmap`; We prefixed the repository name with `r/` to indicate that the recipient is a repo.

