---
id: register-repository
title: Register a Repository
sidebar_label: Register a Repository
description: >-
  This page describes how to register an existing local repository to the
  network.
---

# Register a Repository

Before you can start pushing your local repository to the MakeOS network, you must first register it just like you do when you create a repository on centralized source code hosting platforms. 

You can create a repository via the CLI  or within a JavaScript console session.

## Using The CLI

First, you must create an account key that will be used to sign the transactions. You can skip this set if you already have a key.

{% tabs %}
{% tab title="Bash" %}
```bash
kit key create
```
{% endtab %}

{% tab title="Output" %}
```
- Address: os1m4aaslnzmdp4k3g52tk6eh94ghr547exvtcrkd
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Registering a repository on the network will cost a small fee. You will need to have some test coins sent to your key. If you are [running a private network](../../intro/setup-private-net.md), the `dev.accountKey` can be used in this example. If you are connected to our testnet, you can learn how to request for test coins [here](../../intro/get-test-coin.md).
{% endhint %}

{% hint style="info" %}
See the [Key Guide](../keys.md) to learn more about keys.
{% endhint %}

Next, let us create a transaction to register a repository named `express` to be created. 

{% tabs %}
{% tab title="Bash" %}
```bash
kit repo create "express" \
   --signing-key="os1m4aaslnzmdp4k3g52tk6eh94ghr547exvtcrkd" \ 
   --fee=1.51
```
{% endtab %}

{% tab title="Output" %}
```
- Name: r/express
- Hash:0x14453068c8d4a9db5ccd3f78a...fbe9a9131aa03818a1ee9469a
```
{% endtab %}
{% endtabs %}

We use `--signing-key` flag to set the address of the key, we created earlier. This is the key that will pay the transaction and registration fees. We also set the transaction fee using the `--fee` flag.

{% hint style="info" %}
`--signing-key` can also take the keystore index of the key. 
{% endhint %}

## Using The Console

Like the CLI example, let us create a repository name `express`. In the console, call `repo.create` method to register a new repository:

{% tabs %}
{% tab title="JavaScript" %}
```javascript
repo.create({ name: "express", fee: "1", value: "0"}, dev.accountKey)
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
  "address": "r/express",
  "hash": "0xfc2e2fb9668271f30fa9bcec...28d0e376e4ff6d33ec68363c"
}
```
{% endtab %}
{% endtabs %}

`repo.create` is passed an object that contains the properties of the transaction such as:

* The name of the repository.
* The amount of fees we are willing to pay.
* The amount of Latinum coins we want to add to the repository's balance account.  If set to a non-zero value, the amount is deducted from the signing account and credited to the repository.

The `repo.create` is also passed the private key that will be used to sign the transaction and pay any fee or deductions. For this example, we use the developer account key that includes test coins. The developer key is only available in the testnet or a private development network. 

If you want to use a key on the keystore instead of the `dev.accountKey`, replace it with `user.getKey(accounts[0],"passphrase")`.

where:

* `accounts[0]` : is the key at index 0 in the Keystore. Alternatively, you can use the address of the key. 
* `passphrase`: is the passphrase used to unlock the key. If not provided, a prompt will be initiated to request for it.

