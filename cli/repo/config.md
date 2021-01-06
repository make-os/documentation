---
id: config
title: Configure Repository
sidebar_label: config
description: Configure a repository.
---

# config

The `config` command configures a repository for easy interaction with a MakeOS remote server. The command sets sensible defaults that aim to make it easy for new users to start pushing to their remote repositories. It performs the following actions:

* Adds a remote named `origin` that points to the local address of a MakeOS remote `127.0.0.1:9002`. 
* Configures a signing key at `user.signingKey` to be used for signing git references. 
* If a passphrase for unlocking the signing key is provided, it will attempt to start a cache service and store the passphrase for 24 hours in memory.
* Sets `post-commit` and `pre-push` git hooks for automatic signing.
* Sets transaction information \(e.g fees, nonce etc\).

{% hint style="info" %}
The command stores config options in the repository's `.git/config` file.
{% endhint %}

### Usage

```bash
kit repo config [options] <repodir>
```

```text
Usage:
  kit repo config [flags] [<directory>]

Aliases:
  config, set

Flags:
  -f, --fee float                 Set the network transaction fee
  -h, --help                      help for config
      --no-hook                   Do not add git hooks
  -n, --nonce uint                Set the next nonce of the signing account signing
      --pass-agent-port string    Specify the port the passphrase agent will use (default "9004")
      --pass-ttl string           The cache duration of signing key passphrase (default "24h")
  -k, --push-key string           Specify the push key (defaults to signing key)
  -r, --set-remote strings        Set one or more remotes
  -u, --signing-key string        Address or index of local account to use for signing transaction
  -p, --signing-key-pass string   Passphrase for unlocking the signing account
  -v, --value float               Set transaction value
```

### Arguments

* `repodir` - Path to the repository that needs to be configured.

### Options

* `-k, --push-key` - Set the address or index of a key in the keystore to use for signing push requests.
* `-r, --set-remote` - A comma-separated list of remote URLs to add to the repository. e.g `origin https://remote.com/r/repo, backup https://backup-remote.com/ns/repo`.
* `--no-hook` - Prevents the command from adding git `pre-push` and `post-commit` hooks. 
* `--no-sign` - When set to true, hooks that enable automatic signing will not be configured \(Default: false\).
* `-o, --print-out` - \(Optional\) Print’s out additional config scripts that cannot be executed from within the call process. The output is meant to be evaluated. 
* `-h, --help` - Prints out a help message.

#### Transaction Options

* `-f, --fee` - The amount of coins to pay as the transaction fee. It will be deducted from the signer's account.
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signer's account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

**Passphrase Management**

* `--pass-agent-port` - The port the passphrase agent will use if it is started.
* `--pass-ttl` - The amount of time to store the passphrase in the agent. Accepts duration in the following example format `10s`, `2h`, `4m`.

### Example

* Configure the repository in the current working directory. The example below sets the signing key to a key at index `0` on the keystore. It sets the fee to be paid for push transactions and finally, it sets the git remote. 

```bash
kit repo config    \
    -u=0            \                       # set signing key to key at index 0
    -f=1.51         \                       # set fee for every push to 1.51 coins
    -r="origin https://remotexyz.com/r/repo"       # set remote URL 
```

