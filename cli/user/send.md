---
id: send
title: Send Coins
sidebar_label: send
---

# send

The `send` command creates a transaction that transfers coins from an account to another account or repository.

### Usage

```bash
kit user send [options] <address>
```

```text
Usage:
  kit user send [flags] <address>

Flags:
  -f, --fee float                 Set transaction fee to pay to the network
  -h, --help                      help for send
  -n, --nonce uint                Set the next nonce of the signing account signing
  -u, --signing-key string        Address or index of local account to use for signing transaction
  -p, --signing-key-pass string   Passphrase for unlocking the signing account
  -v, --value float               Set the amount of coin to send
```

### Arguments

* `address` - The recipient address. Can be a user address or a repository address. A namespace URI pointing to a repository or a user address can also be used. 

### Options

* `-h, --help` - Prints out a help message.

#### Transaction Options

* `-f, --fee` - The amount to pay as transaction fee. It will be deducted from the signer's account.
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signer's account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

* Create a transaction that transfers `210` coin to `os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u` and pays 1.51 coins as network fee.

{% tabs %}
{% tab title="Bash" %}
```bash
kit user send -u=0 -v=210 -f=1.51 "os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u"
```
{% endtab %}

{% tab title="Output" %}
```
✅ Transaction sent!
 - Hash: 0x8297afee13e9a34d3023867ce0d4ca9e515fd1dd3560d959301436d41da3c116
   Confirmed!
```
{% endtab %}
{% endtabs %}

* Create a transaction that transfers `10` coins to a repo named `myrepo`.

```javascript
kit user send -u=0 -v=210 -f=1.51 "r/myrepo"
```

