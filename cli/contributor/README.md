# contributor

The `contributor` command allows you to add and manage contributors to a repository.

To see a list of sub-commands, run `kit contributor`

```text
Usage:
  kit contributor [flags]
  kit contributor [command]

Available Commands:
  add         Add one or more contributors to a repository or a namespace or both

Flags:
  -h, --help                  help for contributor
      --no.rpc                Disable connection to the JSON-RPC API
      --rpc.https             Force the client to use https:// protocol
      --rpc.password string   Set the RPC password
      --rpc.user string       Set the RPC username
```

## Global Options

### RPC

For methods that require connecting to a running node, Kit will attempt to connect via RPC by default. These are the options to control the connection:

* `--remote.address`  - The address of the RPC server to make connections to. 
* `--rpc.user` - The username to send to the RPC server for authentication.
* `--rpc.password` - The password to send to the RPC server for authentication.
* `--rpc.https` - Enables SSL connection to the RPC server. 
* `--no-rpc` - If this is set, it will prevent the command from connecting to a remote node via JSON-RPC. 

