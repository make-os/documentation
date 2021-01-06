---
id: init
title: Initialize a Repository
sidebar_label: init
---

# init

The `init` command registers a repository, initializes it locally and configures it. It is a combination of `kit repo create`, `git init` and `kit repo config` commands.

### Usage

```bash
kit repo init [options] <name>
```

```text
Usage:
  kit repo init [flags] <name>

Flags:
      --commit.amend              Sign an amended commit (instead of creating a new one) (default true)
  -c, --config string             Specify repository settings or a file containing it
  -f, --fee float                 Set transaction fee to pay to the network
  -h, --help                      help for init
      --no-sign                   Do not enable automatic signing hook
  -n, --nonce uint                Set the next nonce of the signing account signing
  -o, --print-out                 Print out more config to pass to eval()
  -k, --push-key string           Specify the push key (defaults to signing key)
  -r, --remote strings            Set one or more remotes
  -u, --signing-key string        Address or index of local account to use for signing transaction
  -p, --signing-key-pass string   Passphrase for unlocking the signing account
  -v, --value float               The amount of coins to transfer to the repository
```

### Arguments

* `repodir` - Path to the repository that needs to be configured.

### Options

* `-c, --config` - Provide the repository’s governance and access control settings.
* `-k, --push-key` - Set the address or index of a key in the keystore to use for signing push requests.
* `-r, --remote` - A comma-separated list of remote URLs to add to the repository. e.g `origin https://remote.com, backup https://backup-remote.com`.
* `--commit.amend` - When set to true, a new commit will not be created whenever git attempts to sign a branch. Instead, the recent commit is amended \(Default: true\).
* `--no-sign` - If set to true, hooks that enable automatic signing will not be configured \(Default: false\).
* `-o, --print-out` - \(Optional\) Print’s out additional config scripts that cannot be executed from within the execution process \(e.g environment variable updates\). The output should be passed to eval\(\).  
* `-h, --help` - Prints out a help message.

#### Transaction Options

* `-f, --fee` - The number of coins to pay as the network transaction fee. It will be deducted from the signer's account.
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signer's account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

*  Create, initialize and configure a repository named `myrepo`.

```bash
kit repo init "myrepo"     \
    -u=0                   \                    # set signing key to key at index 0
    -f=1.51                \                    # set fee for every push to 1.51 coins
    -r="origin https://remotexyz.com"           # set remote URL
```

