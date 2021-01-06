---
id: note
title: Sign a Note
sidebar_label: note
---

# note

The `note` command signs and creates a push token for a git note reference. The push request token will be pushed to the server, along with the note reference. 

The server relies on valid push tokens to perform authorization and authentication checks.

### Usage

```bash
kit sign note <name> [options]
```

```text
Usage:
  kit sign note <name> [flags]

Flags:
  -h, --help   help for note
```

### Arguments

* `name` - The name of an existing note.

### Options

* `-h, --help` - Prints out a help message.

#### Sign Options

* `-f, --fee` - The number of coins to pay as the network transaction fee. 
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signer's account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

* Create a signed push request token for a note named `summary`

```bash
kit sign note "summary" 
```

