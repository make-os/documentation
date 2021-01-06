---
id: commit
title: Sign a Commit
sidebar_label: commit
---

# commit

The `commit` command signs the recent commit of a branch and creates a push request token that can be added to the push request to the remote server.

### Usage

```bash
kit sign commit [options]
```

```text
Flags:
      --head string       Specify the branch to use as git HEAD
  -h, --help              help for commit
  -m, --merge-id string   Provide a merge proposal ID for merge fulfilment
```

### Options

* `--head` - The name of the branch that needs to be signed. 
* `-m, --merge-id` - Provide the ID of a merge request proposal that the commit fulfils. 
* `-h, --help` - Prints out a help message.

#### Sign Options

* `-f, --fee` - The number of coins to pay as the network transaction fee. 
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signer's account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

* Sign and create a push token for the latest commit.

```text
kit sign commit
```

* Sign the latest commit on the `dev` branch.

```bash
kit sign commit -h "dev"
```

