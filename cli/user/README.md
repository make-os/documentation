# user

The `user` command provides the sub-commands for accessing personal user and account information.

To see a list of sub-commands, run `kit user`

```text
Usage:
  kit user [flags]
  kit user [command]

Available Commands:
  send        Send coins from a user account to another user or a repository account

Flags:
  -h, --help                  help for user
      --rpc.https             Force the client to use https:// protocol
      --rpc.password string   Set the RPC password
      --rpc.user string       Set the RPC username
```

## Global Options

The command includes global options that can be set for all sub-commands.

### Remote API Server

* `--remote.address`  - The address of the Git & RPC remote server.

### RPC

For methods that require connecting to a running node, Kit will attempt to connect via RPC by default. These are the options to control the connection:

* `--rpc.user` - The username to send to the RPC server for authentication.
* `--rpc.password` - The password to send to the RPC server for authentication.
* `--rpc.https` - Enables SSL connection to the RPC server. 

