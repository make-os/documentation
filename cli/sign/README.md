# sign

The `sign` command provides sub-commands that helps you sign git objects \(e.g. tag and commit\) and generate a push token which a MakeOS node will need to authenticate your push requests.

The command, when called without a subcommand will attempt to sign the current branch's latest commit and generate a corresponding push token.  

To see a list of sub-commands, run `kit sign -h`

```bash
Sign a commit, tag or note. Run 'kit sign' to sign the current commit.

Usage:
  kit sign [command] [flags]
  kit sign [command]

Available Commands:
  commit      Sign a commit or branch
  note        Sign a note
  tag         Sign an annotated tag

Flags:
  -f, --fee float                 Set the network transaction fee
      --head string               Specify the branch to use as git HEAD
  -h, --help                      help for sign
      --merge-id string           Provide a merge proposal ID for merge fulfilment
  -n, --nonce uint                Set the next nonce of the signing account signing
  -x, --reset                     Clear existing remote tokens before creating a new one
  -u, --signing-key string        Address or index of local account to use for signing transaction
  -p, --signing-key-pass string   Passphrase for unlocking the signing account
  -v, --value string              Set a value for paying additional fees

Global Flags:
      --dev                       Enables development mode
      --gitpath string            Set path to git executable (default "git")
      --home string               Set the path to the home directory (default "/Users/ncodes/.kit")
      --home.prefix string        Adds a prefix to the home directory in dev mode
      --loglevel stringToString   Set log level for modules (default [])
      --net uint                  Set network/chain ID (default 1)
      --no-colors                 Disables output colors
      --no-log                    Disables loggers
      --profile.mode string       Enable profiling mode, one of [cpu, mem, mutex, block]
      --remote string             Set the default remote name (default "origin")
      --remote.address string     Set the RPC server address (default ":9002")
      --rpc.https                 Force the client to use https:// protocol
      --rpc.password string       Set the RPC password
      --rpc.user string           Set the RPC username

Use "kit sign [command] --help" for more information about a command.
```

## Global Options

The command includes global options that can be set for all sub-commands.

* `-f, --fee` - Set the number of coins to pay as a transaction processing fee. If unset, the value of `user.fee` config option of the current repository will be used.
* `-n, --nonce` - Set the next nonce of the signing account. This is the number of transactions sent by the signing account + 1. If unset, the value of `user.nonce` config option of the current repository will be used.
* `-v, --value` - \(Optional\) Set the number of coins to be transferred from the signing account. If unset, the value of `user.value` config option of the current repository will be used.
* `-r, --remote` - Provide the remote name where the push token will be added to. 
* `-x, --reset` - Clear previous request tokens from the `.git/config` before creating a new one.

### Remote API Server

* `--remote.address`  - The address of the Git & RPC remote server.

### RPC

For methods that require connecting to a running node, Kit will attempt to connect via RPC by default. These are the options to control the connection:

* `--rpc.user` - The username to send to the RPC server for authentication.
* `--rpc.password` - The password to send to the RPC server for authentication.
* `--rpc.https` - Enables SSL connection to the RPC server.  

## Signing

* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction. If unset, the value of `user.signingKey` config option of the current repository will be used.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key. If unset, the value of `user.passphrase` config option of the current repository will be used.

