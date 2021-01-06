---
id: register
title: Register Public Key
sidebar_label: register
---

# register

The `register` command creates a transaction that registers a public key on the network for use as a push key. The public key can be provided as an argument to the command or a key on the keystore can be registered by specifying the key’s address or keystore index.

### Usage

```bash
kit pk register [flags] <publicKey|keyId>
```

```text
Usage:
  kit pk register [flags] <publicKey|keyId>

Flags:
  -f, --fee float                 Set transaction fee to pay to the network
  -c, --feeCap float              Set the maximum fee the key is allowed to spend on fees
  -h, --help                      help for register
  -n, --nonce uint                Set the next nonce of the signing account signing
      --pass string               Specify the passphrase of a chosen push key account
  -s, --scopes strings            Set one or more push key scopes
  -u, --signing-key string        Address or index of local account to use for signing transaction
  -p, --signing-key-pass string   Passphrase for unlocking the signing account
```

### Arguments

* `publicKey|keyId` - Provide the base58 encoded public key or get the public key of a key on the keystore by its key address or index. 

### Options

* `-c, --feeCap` - Specify the amount of fee that can be spent by the public key from the signing key account. 
* `--pass` - Provide the passphrase that will be used to unlock the key matching `key-id`.
* `-s, --scopes` - Prevent the key from being used outside a set of repositories and namespaces.
* `-h, --help` - Prints out a help message.

#### Transaction Options

* `-f, --fee` - The number of coins to pay as transaction fee. It will be deducted from the signer's account.
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

* Send a transaction that registers the public key of a key at index 2 on the keystore.

{% tabs %}
{% tab title="Bash" %}
```bash
kit pk register -f="0.1" -u=1 "2"
```
{% endtab %}

{% tab title="Output" %}
```
✅ Transaction sent!
- Hash: 0x8297afee13e9a34d3023867ce0d4ca9e515fd1dd3560d959301436d41da3c116
- Confirmed!
```
{% endtab %}
{% endtabs %}

* Create a transaction that registers the public key `47yLa42fJsRxGi2G...obSJ9aRjM6j2sBerT4iqef` and limits its scope to a repository called `myrepo` and a namespace called namespace/.

```bash
kit pk register "47yLa42fJsRxGi2GMsdnTqHaRMXUWobSJ9aRjM6j2sBerT4iqef" \
    -f="0.1" \
    -u=1 \
    -s="myrepo" \
    -s="namespace/"
```

