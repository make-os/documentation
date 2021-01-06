# pk

The `pk` command exposes sub-commands for registering and managing push keys on the network.

To see a list of sub-commands, run `kit pk`

```text
Usage:
  kit pk [flags]
  kit pk [command]

Available Commands:
  register    Register a public key on the network

Flags:
  -h, --help                  help for pk
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
* `--no-rpc` - If this is set, it will prevent the command from connecting to a remote node via JSON-RPC. 

