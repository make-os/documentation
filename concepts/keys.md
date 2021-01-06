---
id: keys
title: Keys
sidebar_label: Keys
description: >-
  A key is a cryptographic object used for identifying an asset on the network
  and for signing transactions.
---

# Key

### Overview

The MakeOS network uses Public Key Infrastructure for handling identity, verifying ownership of resources, signing and authorizing actions targeted at these resources. MakeOS uses [Ed25519](https://ed25519.cr.yp.to/) public-key signature system for all signing operations.

## Key Types

There are two types of keys:

### Standard Key

A standard key is an Ed25519 key that can own a Balance Account on the network. A standard key does not become connected to a network Balance Account until it receives an inbound blockchain transaction.

Standard keys are used to sign transactions that transfer the native coin or user-owned assets from one account to another. 

Standard keys own every other resource on MakeOS and can be identified by their unique address which is generated using bech32 address format and begins with `os1`

### PushKey

A push key is used to sign a git push transaction. When a developer is ready to push an update to their repository, they must sign the commit and create an authentication token \(or Push Token\) using a key. 

A PushKey represents a repository contributor. Repository administrators or maintainers can assign privileges and issues to Push Key.

A Standard Key and PushKey both are Ed25519 keys except a Push Key cannot have a balance associated with it. 

A PushKey is created and owned by a Balance Account. A repository admin can be created an Ed25519 key, register it on the network as a PushKey, add it as a contributor to their repository and send the key to an employee.

A PushKey does not pay its own network transaction fees. Instead, the Balance Account that registered it will be responsible for paying any fees incurred by the Push Key. For example, this model is useful for structures where an organization wishes to bear the cost of their employees contributions to a repository of their choosing.

A PushKey can have a fee cap that will prevent it from spending more than a maximum amount of the registrar account balance. It can also be limited to work with one or several repositories. 

A PushKey is identified by a bech32 address prefixed with `pk`.

## Keystore

The Kit client manages a keystore on the machine it is installed on. Ed25519 keys are stored in an encrypted format using a passphrase provided by the node owner.

## Create a Key

Use the `kit key create` command to create a new key

{% tabs %}
{% tab title="Bash" %}
```bash
kit key create
```
{% endtab %}

{% tab title="Output" %}
```
Your new key needs to be locked. Please enter a passphrase.
Passphrase> *****
Repeat Passphrase> *****
✅ Key successfully created!
- Address: os1m4aaslnzmdp4k3g52tk6eh94ghr547exvtcrkd
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The new key file can be found in the keystore in`$HOME/.kit/keystore.`
{% endhint %}

You will be prompted to provide a passphrase which will be used to encrypt the new key. You can skip the interactive prompt by providing your passphrase directly using the`--pass` flag. 

## Create a Key to Use as a Push Key

A PushKey is also created using the`kit key create` command but with the addition of the `--push` flag. 

{% tabs %}
{% tab title="Bash" %}
```bash
kit key create --push
```
{% endtab %}

{% tab title="Output" %}
```
Your new key needs to be locked. Please enter a passphrase.
Passphrase> ******
Repeat Passphrase> ******
✅ Key successfully created!
- Address: pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpxaa77t
```
{% endtab %}
{% endtabs %}

The `--push` flag will create a regular ed25519 key with keystore type set to `push`. This makes it possible to distinguish keys dedicated for pushing to a repository.

## Get a Key

You can get or inspect a given key using the `kit key get` command.

{% tabs %}
{% tab title="Bash" %}
```bash
kit key get os1m4aaslnzmdp4k3g52tk6eh94ghr547exvtcrkd
```
{% endtab %}

{% tab title="Output" %}
```
Passphrase> *****
✅ Key revealed successfully!
- User Address: os1m4aaslnzmdp4k3g52tk6eh94ghr547exvtcrkd
- Push Address: pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpxaa77t
- Public Key: 48jVDAtY16aXwiccMvCT1UHawWvvoSTDJ7e6hHwM2K3wJvgn5sK
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The command takes the _address of the key_ or the _keystore index_ of the key as an argument.
{% endhint %}

By default, the private key will not be returned in the output. Use the `--show-key` flag to force the private key to be rendered. 

{% hint style="info" %}
Both public and private keys are base58 encoded. This is the format all nodes will expect the keys to be represented in. 
{% endhint %}

## List all Keys on the Keystore

To see a list of keys in your keystore, use the `kit key list`command. 

{% tabs %}
{% tab title="Bash" %}
```bash
kit key list
```
{% endtab %}

{% tab title="Output" %}
```
       Address                                    Date Created    Tag(s)       
  [0]  os1m4aaslnzmdp4k3g52tk6eh94ghr547exvtcrkd  1 week ago                                    
  [1]  pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpxaa77t  1 week ago      unprotected
```
{% endtab %}
{% endtabs %}

This command outputs both regular and PushKeys. 

Keys with an `unprotected` tag are those that were not created with a unique passphrase. All keys are encrypted but unprotected keys are encrypted with a default key which is equivalent to not adding a key at all.

{% hint style="warning" %}
Always use a strong passphrase to lock your keys.
{% endhint %}

## Import Keys

You may need to import a private key from a different machine. Use the `import` the command to import an existing base58 encoded private key into your local keystore:

{% tabs %}
{% tab title="Bash" %}
```bash
kit key import "wetT9rgtetCHJ...GmzRUPU1SmrfNSy4j7DDJ"
```
{% endtab %}

{% tab title="Output" %}
```
Passphrase> ******
Repeat Passphrase> ******
✅ Key imported successfully!
- Address: pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7
```
{% endtab %}
{% endtabs %}

