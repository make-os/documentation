---
id: quickstart
title: Quick Start
sidebar_label: Quick Start
description: >-
  This quick start guide will describe how to set up your local node and connect
  to a network.
---

# Quick Start

## Initialization

{% hint style="info" %}
#### Requires Kit

If you have not installed the Kit client, check the previous [page](install-kit.md) to learn how to install it.
{% endhint %}

The first thing to do is to initialize your machine. This process will create the necessary directories, files and configurations required to run a MakeOS node. 

Open a terminal and run this command:

```bash
kit init --v1
```

The `init` command will set up Kit’s application directory and create the configuration needed to operate a MakeOS node. These data directory of a node can be found in `$HOME/.kit`:

The flag `--v1` applies the network preset that configures your node for the Testnet \(v1\). Without the flag, your node will be configured for the Mainnet which is not live at the moment.

```bash
ls $HOME/.kit 
1 accounts extensions kit.yml

ls $HOME/.kit/config 
addrbook.json genesis.json priv_validator_key.json config.toml node_key.json
```

## Join the network

To get your node to join the public network, run:

```bash
kit start --rpc.on
```

{% hint style="info" %}
#### Turn on RPC service 

The **`--rpc.on`** flag turns on RPC service allowing you to attach to the node.
{% endhint %}

Kit will connect to the network automatically and begin to fetch and execute blocks till it is completely synchronized with the network. Kit connects to seed nodes embedded in the binary and managed by us.

The seed nodes in the binaries we distribute will allow you to quickly and painlessly connect to the network as soon as you start Kit.

However, if you want to connect to a specific node of your choice, use the `--node.addpeer` flag to add one or more peer addresses:

```bash
kit start --node.addpeer="<id-of-node>@127.0.0.1:9000"
```

## Start in console mode

Kit provides a JavaScript console environment that allows you to create custom instructions and execute operations not natively or conveniently provided via the CLI interface.

On the console, you can perform query operations, create transactions, execute custom scripts, perform RPC operations and more.

To start a node in console mode, open a new terminal window and run:

```bash
kit console --rpc.on
```

The command will start a console session that allows you to execute JavaScript expressions and scripts:

```bash
Welcome to the JavaScript Console! 
Client:0.0.1, Protocol:1, Commit:4e522ab9a9...568f6abcae, Go:go1.14.5 
type '.exit' to exit console

> 2 + 2
4 
```

The command above is like `kit start`, except it also runs the JavaScript console where you can write and execute JavaScript expressions.

## Attach to a node

Kit can attach to and interact with a running node via RPC. In attach mode, a JavaScript console is started and connects to the RPC service of a local or remote node, allowing you to query and execute operations against it.

If you already have a node running on the default RPC address and port, you can attach to it using the `kit` command:

```bash
kit attach
```

However, if the node is running on a remote server, you can specify the remote address of the server using the `--remote.address` flag:

```bash
kit attach --remote.address="10.45.22.21:9002"
```

Use `--rpc.user` and `--rpc.password` to set RPC username and password.

{% hint style="warning" %}
You may find that some methods available in the console mode are non-functional in attach mode. We are working to bring the attach mode into parity with the console mode
{% endhint %}

## Create a Repository.

{% page-ref page="get-test-coin.md" %}

{% page-ref page="../concepts/repository/initialize-repository.md" %}

