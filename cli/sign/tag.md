---
id: tag
title: Sign a Tag
sidebar_label: tag
---

# tag

The `tag` command creates a signed push token that references an existing tag. The push token will be pushed along with the annotated tag reference. 

A MakeOS server relies on push tokens to perform authorization and authentication checks before processing the pushed reference. 

### Usage

```bash
kit sign tag [options] [-- [git options]]
```

```text
Usage:
  kit sign tag <name> [flags]

Flags:
  -h, --help         help for tag
```

### Arguments

* `name` - The name of the tag.

### Options

* `-h, --help` - Prints out a help message.

#### Sign Options

* `-f, --fee` - The number of coins to pay as the network transaction fee. 
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signer's account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

* Create and sign a tag named `v0.0.1` with the message `initial version`.

```bash
# Create an annotated tag
git tag -a v0.0.1 -m "initial version"

# Sign and create a push token that references the tag
kit sign tag v0.0.1
```

