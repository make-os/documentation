# repo

The `repo` command provides the ability to create a repository, configure it for convenient operability with the network and manage its governance.

To see a list of sub-commands, run `kit repo`

```text
Usage:
  kit repo [flags]
  kit repo [command]

Available Commands:
  config      Configure repository settings
  create      Create a repository
  hook        Handles git hook events
  init        Register a repository, initialize and configure it locally.
  vote        Vote for or against a proposal

Flags:
  -h, --help                  help for repo
      --rpc.https             Force the client to use https:// protocol
      --rpc.password string   Set the RPC password
      --rpc.user string       Set the RPC username
```

## Global Options

The command includes global options that can be set for all sub-commands.

### Remote

* `--remote.address` - The address where the remote server will listen for git requests.

### RPC

For methods that require connecting to a running node, Kit will attempt to connect via RPC by default. These are the options to control the connection:

* `--rpc.user` - The username to send to the RPC server for authentication.
* `--rpc.password` - The password to send to the RPC server for authentication.
* `--rpc.https` - Enables SSL connection to the RPC server. 

