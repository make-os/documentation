---
id: start
title: Start
sidebar_label: start
---

# start

The `start` command starts the Kit client and connects it to the network. It learns about the network and finds other peers by connecting to a set of embedded seed nodes in the client. 

The seed nodes shares the addresses of other peers on the network and quickly disconnects. With the addresses received, the node improves its connection to the network by connecting to more peers.

## Usage

```text
kit start [options]
```

```text
```txt
Launch the node to join the network.

Usage:
  kit start [flags]

Flags:
      --dht.addpeer string             Register bootstrap peers for joining the DHT network
      --dht.address string             Set the DHT listening address (default "127.0.0.1:9003")
      --dht.on                         Run the DHT service and join the network (default true)
  -h, --help                           help for start
      --node.addpeer string            connect to one or more persistent node
      --node.address string            Set the node's p2p listening address (default "127.0.0.1:9000")
      --node.exts strings              Specify an extension to run on startup
      --node.extsargs stringToString   Specify arguments for extensions (default [])
      --node.validator                 Run the node in validator mode
  -t, --repo.track strings             Specify one or more repositories to track
  -u, --repo.untrack strings           Untrack one or more repositories
  -x, --repo.untrackall                Untrack all previously tracked repositories
      --rpc.authpubmethod              Enable RPC authentication for non-private methods
      --rpc.disableauth                Disable RPC authentication
      --rpc.on                         Start the RPC service
      --rpc.password string            Set the RPC password
      --rpc.tmaddress string           Set tendermint RPC listening address (default "127.0.0.1:9001")
      --rpc.user string                Set the RPC username
```

## Options

### Node

* `--node.address` - The address the node will bind and listen to for incoming connections.
* `--node.addpeer` - Provide a comma-separated list of node addresses to connect to.
* `--node.exts` - Specify an extension to run when the node starts.
* `--node.extsargs` - Provide arguments for extensions.
* `--node.validator` - Run the node in validator mode. This will prevent your node from taking part in host operations. 

### Remote

* `--remote.address` - The address where the remote server will listen for git requests.

### RPC

* `--rpc.on` - Starts the RPC server on the default address. By default, the server is not started.
* `--rpc.authpubmethod` - Force the RPC server to require authorization check for calls targeting public RPC methods.
* `--rpc.disableauth` - Prevents the RPC server from performing authorization checks of incoming requests.
* `--rpc.user` - The RPC user to use for basic authorization.
* `--rpc.password` - The RPC password to use for basic authorization.
* `--rpc.tmaddress` - The address where the Tendermint RPC server listens for incoming RPC requests coming from Kit. 

### DHT

* `--dht.on` - Starts the DHT server. It will connect to the DHT seed nodes embedded into the client. 
* `--dht.address` - Set the address where the DHT will bind to and listen for incoming connections.
* `--dht.addpeer` - Provide a comma-separated list of DHT node address to connect to. 

## Example

* Start the node and its RPC service.

```bash
kit start \
    --rpc.on \                            # Turns on RPC service
    --remote.address=:6000 \              # Sets the RPC and Remote server listen address.  
    --rpc.user admin \                    # The RPC server basic auth username
    --rpc.password admin \                # The RPC server basic auth password
    --dht.addpeer=/ip4/127.0.0.1/tcp/7003/p2p/12D3KooWENHGhd6853kiLQLo5g7zLkMrdbma5K2CYwdSpbNCNk3t # Adds the address to the DHT bootstrap peer list. 
```

