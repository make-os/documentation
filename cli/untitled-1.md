---
id: attach
title: Attach
sidebar_label: attach
---

# attach

The `attach` command is used to start a JavaScript console that connects to an already running local or remote Kit node.

### Usage

```bash
kit attach [options]
```

```text
Start a JavaScript console that attaches to a local or remote node

Usage:
  kit attach [flags]

Flags:
      --exec string           Execute the given JavaScript code
  -h, --help                  help for attach
      --remote.address string Set the RPC server address to connect to (default "127.0.0.1:9002")
      --rpc.https             Connect using HTTPS protocol
      --rpc.password string   Set the RPC password
      --rpc.user string       Set the RPC username
```

### Options

* `--exec` - Executes a JavaScript source code and exit. If a path is provided, it is read and executed.  
* `--remote.address`  - The address of the Git & RPC remote server.
* `--rpc.https` - Indicates that SSL should be used when connecting to the node.
* `--rpc.user` - Provide the username of the server for basic authentication.
* `--rpc.password` - Provide the password of the server for basic authentication.
* `-h, --help` - Print out a help message.

### Example

* Attach to the local node running on the default `address:port`.

```text
kit attach
```

* Attach to a remote node at the address `rpc.mynode.net:9003`. 

```bash
kit attach --remote.address="rpc.mynode.net:9003" --rpc.user="user" --rpc.password="pass"
```

* Attach to a node and execute a JavaScript expression immediately after attaching.

{% tabs %}
{% tab title="Bash" %}
```bash
kit attach --exec='2+2'
```
{% endtab %}

{% tab title="Output" %}
```bash
> 4 
```
{% endtab %}
{% endtabs %}



