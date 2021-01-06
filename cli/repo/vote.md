---
id: vote
title: Vote on a Proposal
sidebar_label: vote
---

# vote

The `vote` command creates a transaction that votes for or against a repository proposal.

### Usage

```bash
kit repo vote [options] <choice>
```

```text
Usage:
  kit repo vote [flags] <choice>

Flags:
  -f, --fee float                 Set transaction fee to pay to the network
  -h, --help                      help for vote
  -i, --id string                 The unique ID of the proposal
  -m, --mr string                 The unique ID of a merge request
  -n, --nonce uint                Set the next nonce of the signing account signing
  -r, --repo string               The name of the repository
  -u, --signing-key string        Address or index of local account to use for signing transaction
  -p, --signing-key-pass string   Passphrase for unlocking the signing account
```

### Arguments

* `choice` - The vote choice.
  * `0` - No
  * `1` - Yes
  * `2` - NoWithVeto
  * `3` - Abstain

### Options

* `-r, --repo` - The repository name on which the proposal exists.
* `-i, --id` - The unique ID of the proposal that will be voted on.
* `-m, --mr` - Like `--id`, but use this if the proposal is a merge request. It will add the necessary merge request proposal prefix. 
* `-h, --help` - Prints out a help message.

#### Transaction Options

* `-f, --fee` - The number of coins to pay as the network transaction fee. It will be deducted from the signer's account.
* `-n, --nonce` - The next nonce of the signer's account \(current nonce +  1\). 
* `-v, --value` - The number of coins to transfer from the signer's account.
* `-u, --signing-key` - The address or index of a key that will be used to sign the transaction.
* `-p, --signing-key-pass` - The passphrase that will be used to unlock the signing key.

### Example

* Creates a transaction that votes `Yes` to a proposal with the ID = `101` in a repository named `myrepo`.

{% tabs %}
{% tab title="Bash" %}
```bash
kit repo vote 1 -i=101 -u=0 -f=1.51 -r="myrepo"
```
{% endtab %}

{% tab title="Output" %}
```
> ✅ Transaction sent!
  - Hash: 0x8297afee13e9a34d3023867ce0d4ca9e515fd1dd3560d959301436d41da3c116
    Confirmed!
```
{% endtab %}
{% endtabs %}

