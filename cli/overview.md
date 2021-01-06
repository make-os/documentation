---
id: overview
title: Lobe Commands (CLI)
sidebar_label: Overview
---

# Overview

Kit is the reference client of the MakeOS network being developed by the Make One team. It is being developed with the Go programming language. 

Kit aims to provide a client that allows you to easily interact with the network, manage keys and create third-party applications via an RPC API and an extension system.

It provides a single command-line application named `kit` that returns non-zero errors when a command produces an error. You can use `-h` or `--help` to get descriptive help text for every command.

To see a list of commands, run `kit` :

```text
Kit is the official client for the MakeOS network

Usage:
  kit [flags]
  kit [command]

Available Commands:
  attach      Start a JavaScript console attached to a node
  console     Start a JavaScript console and connect the node to the network
  contributor Manage repository contributors
  help        Help about any command
  init        Initialize the application.
  issue       Create, read, list and respond to issues
  key         Create and manage your account and push keys.
  mr          Create, read, list and respond to merge requests
  pk          Register and manage network push keys
  repo        Create, find and manage repositories
  sign        Sign a commit, tag or note and generate a push request token
  start       Launch the node to join the network.
  tx          Create and read transaction data or status
  user        Access and manage a user's personal resources

Flags:
  -v, --version              Print version information
      --dev                  Enables development mode
      --gitbin string        Set path to git executable (default "/usr/bin/git")
      --home string          Set the path to the home directory (default "/Users/example/.kit")
      --home.prefix string   Adds a prefix to the home directory in dev mode
      --net uint             Set network/chain ID (default 1)
      --no-colors            Disables output colors
      --no-log               Disables loggers
  -h, --help                 help for kit

Use "kit [command] --help" for more information about a command.
```

## Global Options

Kit includes persistent flags that are settable from any command. These flags allow you to set things like the home directory, git executable path and so on.

### Usage

`kit [options]`

### Options

* `-v, --version` - Returns the version information of the client.
* `--dev` - Turns on development mode.
* `--gitbin` - Provide the path to git executable for performing git operations on repositories.
* `--home` - Set the data directory of the Kit client. By default, the home data directory will be created in the machine’s home directory with the name `.kit`. In dev mode, it will be named `.kit_dev`. If `--home.prefix` is set, it will be `.kit_prefix`. 
* `--net` - Set the unique network ID. This will determine what network the client can interact with. 
* `--no-colors` - Prevent the use of colors in the command output. 
* `--no-log` - Disable Kit and Tendermint loggers. 
* `-h, --help` - Print out a help message. 

## Environment Variables

Kit allows flags of all commands to be configured via the command line. For instance, to set the`--home` from the environment, use the variable `KIT_HOME` where `KIT_` is the namespace and `HOME` is the target flag.

