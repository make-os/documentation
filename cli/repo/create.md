---
id: create
title: Create
sidebar_label: create
---

# create

The `create` command creates a transaction that will register a new repository on the network.

It requires a signing key from the keystore to sign the transaction. The passphrase to unlock the selected signing key can be provided via `-p` flag or a prompt will be started to ask for it.

### Usage

```text
kit repo create [options]
```

```text
Usage:
  kit repo create [flags] <name>

Flags:
  -c, --config string             Specify repository settings or a file containing it
  -f, --fee float                 Set transaction fee to pay to the network
  -h, --help                      help for create
  -n, --nonce uint                Set the next nonce of the signing account signing
  -u, --signing-key string        Address or index of local account to use for signing transaction
  -p, --signing-key-pass string   Passphrase for unlocking the signing account
  -v, --value float               The amount of coins to transfer to the repository
```

### Arguments

* `name` - The unique name of the repository.

### Options

* `-c, --config` - Provide the repository’s governance and access control settings.
* `-h, --help` - Prints out a help message.

#### Transaction Options

* `-f, --fee` - The number of coins to pay as the transaction fee. It will be deducted from the signer's account.
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signer's account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

The example below creates a transaction that will register a repo named `myrepo` and transfers 120 units of coins to its balance account.

{% tabs %}
{% tab title="Bash" %}
```bash
kit repo create "myrepo" -u=0 -f=1.51 -v=120
```
{% endtab %}

{% tab title="Output" %}
```
✅ Transaction sent!
 - Name: r/myrepo
 - Hash: 0x8297afee13e9a34d3023867ce0d4ca9e515fd1dd3560d959301436d41da3c116
 - Confirmed!
```
{% endtab %}
{% endtabs %}

