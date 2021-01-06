---
id: add
title: Add a Contributor
sidebar_label: add
---

# add

The `add` command creates a repository proposal transaction that will add one or more push keys as contributors of a repository, namespace or both.

### Usage

```bash
kit contributor add [options]
```

```text
Usage:
  kit contributor add <pushKeys> [flags]

Flags:
  -f, --fee float                 Set transaction fee to pay to the network
      --feeCap float              Max. amount of repo balance the contributor(s) can spend on fees
      --feeMode int               Specify who pays the fees: 0=contributor, 1=repo, 2=repo (capped)
  -h, --help                      help for add
  -r, --name string               The name of the target repository
      --namespace string          Add contributor(s) to the given repo-owned namespace
      --namespaceOnly string      Only add contributor(s) to the given repo-owned namespace
  -n, --nonce uint                Set the next nonce of the signing account signing
      --policies string           Set repository policies
      --id string                   The unique proposal ID (default: current unix timestamp)
  -u, --signing-key string        Address or index of local account to use for signing transaction
  -p, --signing-key-pass string   Passphrase for unlocking the signing account
  -v, --value float               The proposal fee to be paid if required by the repository
```

### Arguments

* `pushKeys` - A comma-separated list of push keys that will be added as contributors.

### Options

* `id` - A unique number to be used as the ID of the proposal that will be created on the target repository.
* `name` - The name of the target repository where the push key will be added as a contributor.
* `namespace` - Also add the push key as a contributor to the given namespace. The namespace must be owned by the target repository.
* `namespaceOnly` - If set, the push key will only be added to the namespace. It will not be added as a contributor to the target repository. 
* `policies` - Specify contributor policies for the push key. e.g. `{"obj": "refs/heads/master", "act": "write"}`.
* `feeMode` - `Number`: The fee mode determines who pays the fees whenever a contributor performs a push operation. There are 3 fee mode options: 
  * 0: Contributor pays for their fees.
  * 1: Repository pays for contributors fees. 
  * 2: Repository pays a capped amount of contributors fees. 
* `--feeCap` - Specify the amount of fee that can be spent by the public key from the signing key account. 
* `--pass` - Provide the passphrase that will be used to unlock the key matching `key-id`.
* `-s, --scopes` - Prevent the key from being used outside a set of repositories and namespaces.
* `-h, --help` - Prints out a help message.

#### Transaction Options

* `-f, --fee` - The number of coins to pay as transaction fee. It will be deducted from the signer's account.
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signers account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

* Creates a proposal to add `pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7` as a contributor to a repository named `myrepo`.

```bash
kit contributor add "pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7" \
    -r="myrepo"                                                 \
    -u=0                                                        \
    -f="0.1"
```



