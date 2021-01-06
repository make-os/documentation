---
id: init
title: Init
sidebar_label: init
---

# init

The `init` command is the first command to call when setting up a new MakeOS node using the Kit client. Its purpose is to create the necessary directories, files and seed them with default configuration values required to connect and interact with the MakeOS network.

## Usage

```text
kit init [options]
```

```text
This command initializes the node's data directory and config files.

Usage:
  kit init [flags]

Flags:
  -s, --gen-state string       Specify raw or path to genesis state
  -t, --gen-time uint          Specify genesis time (default: current UTC time)
  -h, --help                   help for init
      --v1                     Configure the node for testnet v1
  -k, --validator-key string   Private key to use for validator role
  -v, --validators strings     Public key of initial validators
```

## Options

* `-s, --gen-state` - Specify a path to a JSON file containing the genesis state.
* `-t, --gen-time` - Provide the Unix timestamp when the blockchain will start.
* `-h, --help` - Print out help message for the command.
* `--v1` - Apply network preset for testnet v1.
* `-k, --validator-key` - The base58 encoded private key to use as the node’s validator private key.
* `-v, --validators` - A comma-separated list of base58 encoded public keys of the initial validators.

## Examples

The example below initializes the node in development mode setting the genesis validators using the `-v` flag, its validator key using `-k` flag and the genesis time with the `-t` flag. 

{% tabs %}
{% tab title="Bash" %}
```bash
kit init --dev --home.prefix mynode \
    -v 489XdyeZjDqx4GQiegutACHpeJb89ZBL5K3XEmfZTJtr1CcPJy1,\
        49Ejroft49qZjvf8aAbUfhJEXtAy4L9W5rotS1z8v494EbjxbBe, \
        47p1YrT93a5m33SHsqH3CU1n3vYW7CR2bybjd4SNVicYLQ1CcSC \
    -k wLPUBRgJ1kQ73AVaqfZ9vpzikh4J34qxdsAbDaQAK4ic7JJZkLfbNuufL8eXXmXdTR6eei1G68RYw8kG7gJ8qwmZC27EuQ \
    -t 1595700581
```
{% endtab %}

{% tab title="Output" %}
```bash
I[2020-08-19|14:42:12.921] Generated private validator keyFile=/Users/alice/.lobe_mynode/1/config/priv_validator_key.json stateFile=/Users/alice/.lobe_mynode/1/data/priv_validator_state.json 
I[2020-08-19|14:42:12.921] Generated node key path=/Users/alice/.lobe_mynode/1/config/node_key.json 
I[2020-08-19|14:42:12.922] Generated genesis file path=/Users/alice/.lobe_mynode/1/config/genesis.json 
```
{% endtab %}
{% endtabs %}

