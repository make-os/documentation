---
id: initialize-repository
title: Initialize a Repository
sidebar_label: Initialize a Repository
description: >-
  The last page describes how to register an existing local repository to the
  network. This page details how to initialize a new local repository and at the
  same time, register it on the network.
---

# Initialize a New Repository

On this page, you will learn how to register and initialize a new repository using the `repo init` command. This command performs the following operations so you don’t have to:

* Registers a repository on the network.
* Initialize a local repository.
* Adds the local node as a remote.
* Configures the repository for pushing and pulling.

## Create a key

{% hint style="info" %}
Feel free to skip this section if you already have a key. If not see [Key](../keys.md) page to learn more.&#x20;
{% endhint %}

Registering a new repository requires an identity. On MakeOS, keys offer a way for users to create an identity, authorize transactions, receive/send value and pay for services. You can create a key using the command below:

{% tabs %}
{% tab title="Bash" %}
```bash
kit key create
```
{% endtab %}

{% tab title="Output" %}
```
Passphrase> ***
Repeat Passphrase> ***
✅ Key successfully created!
- Address: os150xvxt559v4n5530tw9y5tk2ghfflsczqxcdja
```
{% endtab %}
{% endtabs %}

You will be asked to provide a passphrase that will be used to encrypt the key in the keystore.&#x20;

## Get Test Coins

{% hint style="info" %}
You can skip this section if you already have a key with some test coins.
{% endhint %}

Like most blockchains, MakeOS require users to pay a small fee to have transactions quickly processed. To continue following this guide, you will need some test coins in your newly created key. Copy your new address and go to our Testnet faucet to request for [test coins](https://makeos.org/pages/faucet).

## Initialize a Repository

{% hint style="info" %}
We are using **`express`** as the name of our test repository. If you are connected to the test network, you may need to use a different name since the name may no longer be available.
{% endhint %}

It is time to create your repository. The example below will register a new repository named `express` on the MakeOS network.&#x20;

It will also initialize the repository in the current directory and configure it to make it easy for you to run git sign, fetch and pushing operations.

{% tabs %}
{% tab title="Bash" %}
```bash
kit repo init "express" \
    -u="os150xvxt559v4n5530tw9y5tk2ghfflsczqxcdja" \
    -f="0.01"
```
{% endtab %}

{% tab title="Output" %}
```
Passphrase> ******
✅ Transaction sent!
 - Hash: 0x9057bb672bdaa0cc2e45...ae7049d80f90517698f39f2d93c
   Confirmed!
Step 2: Initialized repository
Step 3: Configured repository
Success! Created a new repository express
```
{% endtab %}
{% endtabs %}

The `-u` flag specifies the address of your new key; This key is known as the _signing key_. It is used to sign the transaction and will pay any network fee and deduction. You will be asked for the passphrase that will be used to unlock the signing key.

{% hint style="info" %}
You can provide the keystore index of your signing key to `-u` instead of a full address.
{% endhint %}

By default, the signing key will be added as the first contributor (or Push Key) to the repository. It will also be used to sign future push requests.

The `-f` flag specifies the amount of fee you are willing to pay from your signing key to the network in other to create the repository. This fee will also be used as the transaction fee for future push requests.&#x20;

You can change the fee by setting `user.fee` in git config, by running:

* `kit repo config -f=<your fee>` or&#x20;
* `git config user.fee <your fee>`.

See the [init command](https://app.gitbook.com/s/-MMaaTKhGv9TFS4221Rr/concepts/repository/concepts/repository/commands/repo/init.md) documentation for more options.

## Start Pushing

By default, the `init` command will set `origin` remote to `127.0.0.1:9002` where it expects a Kit node to be running. At this point, we are assuming that you already have a running local node.&#x20;

Every time you add a commit, Git will fire the  `post-commit` hook which will cause Kit to sign your new commit and create a fresh push token that will be used to authenticate your push request.

Go ahead and create a commit and then push it.&#x20;

```bash
git push origin <branch>  # Change <branch> to your own branch name 
```

{% hint style="info" %}
You can change the remote URL it at any time by going to `.git/config` to edit remote's URL or using `git remote set-url <remote> <url>` command. &#x20;

See the [Quick Start Guide](https://app.gitbook.com/s/-MMaaTKhGv9TFS4221Rr/concepts/repository/intro/quickstart.md) to learn how to start up a local node.
{% endhint %}

## Seed Remote Nodes

To create a permission-less, un-censorable and un-stoppable code collaboration platform, it is important that users are able to run their own remote node. However, it can take some minutes for a remote node to sync up with the network causing users to wait for some time to push updates. We provide seed remote nodes for users who cannot wait to sync with the network or do not want to run or manage their own remote node.

### Seed Remote Address

* **s1.seeders.live:9002**
* **s2.seeders.live:9002**

{% hint style="info" %}
To make it easy for users to run their own node, we are working to make Kit support light client and fast sync modes that synchronizes with the network at a very fast rate and tracks only pre-selected repositories.
{% endhint %}

### Add Seed Remote

You can add the seed remote URL to your repository using `git remote` command:

```bash
git remote add seed "http://s1.seeders.live:9002/r/<your-repo>"
```

Replace `<your-repo>` with the name of your own repository.
