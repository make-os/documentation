---
id: how-it-works
title: How it Works
sidebar_label: How it Works
---

# How it Works

On this page, we provide an overview of the architecture of the MakeOS protocol and how it works. You will learn:

* About the network participants.
* How git push requests are handled.
* Basic protocol economics.
* The consensus mechanism.

{% hint style="warning" %}
**Work In Progress:** This is not an exhaustive specification of the protocol. A proper specification will be released as soon as the protocol and reference client enters a stable state.
{% endhint %}

## Overview

The network is composed of many nodes spread across the globe, connected and working together to perform operations defined in the MakeOS protocol to enable uncensorable, unstoppable software development. There are several participants in this system that work together to achieve the platform’s goals:

### Network Participants

There are 5 network participants namely:&#x20;

1. Account owners.
2. Remote providers.
3. Hosts
4. Validators.
5. Delegators.



## Account Owners

An account is a network resource that can send and receive transactions, has a balance and can be used to identify a network user. Accounts can own network resources and may transfer ownership of these resources to other accounts. An account is associated with a private key which is used to authorize transactions. An account owner is a user that controls an account.

### **Types Of Account Owners**

There are two types of account owners:

#### **1. Balance Account Owner**

A Balance Account owner is a user who owns an account that stores the balance of the native coins and other native resources (such as repositories, push keys and batteries). A Balance Account, like a bank account, has a unique identifier that can be used to receive network resources from other account owners.

#### **2. Push Account Owner (a.k.a Pusher)**

A push account owner (aka _pusher_) is a user who has registered a key on the network solely for signing push transactions (aka _push key_). A user who intends to push updates to a repository must create a push key, register it on the network and add it to the repository before they can successfully push. The pusher can instruct git to sign commits with their push key. Push accounts are usually associated with a Balance Account that may be required to pay network fees when required.

{% hint style="info" %}
MakeOS keys are Ed25519 keys
{% endhint %}

### Remote Provider

A remote provider is someone who runs a Git server for handling git fetch and push requests. Users can add them as git remotes, fetch repositories and push updates to them. The remote server handles incoming push requests by validating the request, authenticating the user, broadcasting a push notification to the rest of the network and finally constructing a push transaction for inclusion into the mempool.

Anyone can run a private remote only they can access or a public one accessible to anyone. Remotes are capable of tracking all repositories on the network and downloading every new update as they are pushed. However, it can be configured to only track selected repositories.

A remote provider is incentivized via transaction fees and block inflation. A remote node will take a fraction of the fees paid by the pusher to cover the cost of providing the service. This is designed to encourage users to run public remote servers.

### Hosts

Hosts are keepers of Git objects. They are tasked with persisting the state of all repositories and must make repository objects available to everyone. Hosts are connected to each other through a distributed hash table network where they announce themselves as providers of Git objects and fetch objects from other hosts.

They are also endorsers of push requests — They receive push request notifications from remote providers, validate and authenticate the requests, download git objects, dry-run git updates and send out endorsements if they are satisfied. A push request notification cannot be used to create a push transaction if a pre-determined number of endorsements have not been received. When a node on the network receives both the push request notification and the required number of endorsements, they can add a push transaction to the mempool.

The host role is network incentivized; It is subsidized by the network via block inflation reward. To become a host, one must deposit a minimum amount of the native coin as a security deposit that may be slashed when bad behaviour is detected. The number of hosts in the network is limited.

Hosts are meant to serve as network-sponsored archival nodes that ensure the continued existence and availability of objects, however, anyone can perform their storage functions by running a full node.

### Validators

Validators are nodes that participate in the consensus system of the network. They are responsible for proposing, validating, voting for blocks and finally executing the transactions in the approved blocks. MakeOS is a Proof-of-Stake blockchain built on top of [Tendermint Core](https://tendermint.com), a BFT consensus engine. At launch, MakeOS will allow a maximum of 100 validators and gradually increase that number over time.

**Anyone can become a validator if:**

* They have enough native coins to stake and become part of the top 100 most staked validators.
* or if they receive enough delegated stake that catapults them into the top 100 most staked validators.

Validator role is an incentivized role — When a validator proposes a block that gets approved, they would receive newly minted native coins as a reward.&#x20;

### Delegators

The validator role requires high performing hardware and technical skills to operate a node successfully over a long period. These requirements prevent many from participating in the coin generation process allowing only a few validators to benefit from it. MakeOS provides a delegate system that allows anyone to delegate their native coins to any active validator or host.

When a user delegates to a validator or a host, they increase the power of the delegate, pushing them further up the ranking list. They will share any rewards received by their delegates at a commission rate determined by the delegate. Likewise, if a delegate is slashed for misbehaviour, their delegators will also be slashed. Delegators must decide carefully who they are backing.

### Push Protocol Walk-through

In this section, we will outline how the protocol works to enable a decentralized repository hosting system. This outline is meant to serve as an overview and not an exhaustive, in-depth specification.

{% hint style="warning" %}
The protocol is still very much a work-in-progress. Parts of it may change before launch.
{% endhint %}

## Push Protocol

These are the protocols a pusher must follow to create a valid push request targeting an existing repository:

1. The Pusher must create an ED25519 keypair.&#x20;
2.  Pusher must create a push key by registering the public key from #1 on the network by creating a&#x20;

    `TxRegisterPushKey` transaction.

    1.  On successful registration, the pusher can now refer to the registered push key using the push address&#x20;

        (a Bech32 address with HRP=push).&#x20;
3. The Pusher may create a repository using `TxRepoCreate` transaction if they do not already have one.
4.  Pusher must add push key as a contributor to the repository at `#3` via a `TxRepoProposalRegisterPushKey` transaction.&#x20;

    This step can be skipped if the repository is configured to consider the creator as the first contributor. &#x20;
5.  Pusher must create and sign a token called a _Push Token_. It is used by the remote and other nodes to perform&#x20;

    authentication, authorization and push integrity checks.
6. Pusher must sign commit with the registered push key.
7. User must push signed commit using `git push`.&#x20;

## Remote

These are protocols a remote must follow to successfully handle a push request from a pusher:

#### **On Push Received:**&#x20;

1. Remote must extract, parse and decode _Push Token_ from the request header.&#x20;
2. Remote must validate and verify the properties of the push token.&#x20;
3. Remote must perform authorization and authentication checks before reading pushed objects.&#x20;
4. On successful auth, the Remote must execute the push update and create a changeset describing how the pushed references changed.&#x20;
5. Remote must compare commit signature header values with push token properties to ensure integrity is maintained.&#x20;
6. Remote must create, sign and broadcast a `PushNote` describing both the old state and new state of the repository. `PushNote` contains:&#x20;
   1. The pushed references changes, nonce, anti-spam fee.&#x20;
   2. Pusher’s _Push Token_ signature to allow other nodes to verify that a push originated from the pusher.&#x20;
   3. Remote’s public key and signature. &#x20;
7. Remote must revert the repository to its previous state.&#x20;
8. Remote must cache the`PushNote` in the pushpool while waiting for endorsements from hosts.&#x20;
9. Upon receiving a pre-defined number of valid endorsements, the Remote must attempt to create, sign and add a `TxPush` transaction to the mempool.

#### **On `TxPush` Confirmed**&#x20;

1. Finalize the repository's state by applying the changes described in the `PushNote`.

## Host

Hosts are responsible for endorsing push notification, archiving and providing git objects while being incentivized by the network. They follow the following protocol:

#### **On PushNote Received:**&#x20;

1. The Host must ensure the target repository was registered.&#x20;
2. The Host must ensure the target repository exists on the filesystem.&#x20;
3. The Host must validate the push note; performing both sanity and consistency checks.&#x20;
4. The Host must perform authorization and authentication checks with the goal to:&#x20;
   1. Ensure that the notification is a reaction to a valid push request.&#x20;
   2. 2\. Ensure that the pusher has the authority to push to the target repository.
5. The Host must download the objects required to apply push note updates to the repository.&#x20;
6. After download, the Host must attempt to apply the updates. If it succeeds:&#x20;
   1. It must revert the repository to its previous state.&#x20;
   2. It must create and broadcast a `PushEndorsement`.&#x20;
   3. If it has received enough `PushEndorsement` for the `PushNote`, it must attempt to create a `TxPush` transaction and add to the mempool.

#### **On `TxPush` Confirmed**&#x20;

1. Finalize the repository's state by applying the changes described in the `PushNote`.

## Validator

In the push request handling cycle, validators are responsible for executing push transactions that made it into a block and have the required minimum endorsements. Validators update the repositories network state to match the one described in the endorsed `PushNote`.

#### **On each `TxPush` received**:

1. &#x20;The Validator must check the push transaction.&#x20;
   1. Must ensure the push note is valid.&#x20;
   2. Must ensure push endorsements are present and valid.&#x20;
2. The Validator must add or updates reference state and nonce on the target repository.&#x20;
3. The Validator must deduct fees.

## Basic Protocol Economics

This section briefly describes the economic concept of the MakeOS network

### Native Currency

MakeOS has a native currency known as _Latinum_. It exists to serve as the base currency for paying fees, staking in various governance processes. It provides a means for the protocol and users to price and pay for network services and ultimately provide security to the network via validator and host staking. There will be a total initial supply of 150,000,000 (150 Million) coins at launch and a 3.5% yearly inflation until the supply reaches 700,000,000 (700 Million).

#### Use case:

* Network security via validator & host staking.
* Spam prevention via fees.
* Unit of account and Medium of exchange within the network.
* For incentivizing network participants for their contributions.



### Repository Coin

A Repository Coin (or RepoCoin) is a native coin for a repository. It is issued by repository owners.&#x20;

They have similar properties to Ethereum’s ERC-20. They are fungible and can be transferred from one account to another.&#x20;

Like Latinum, Repository Coins can be stored in a Balance Account or transferred between accounts.

### Consensus Mechanism

MakeOS is built on [Tendermint Core](https://tendermint.com). Tendermint is a fast, BFT consensus engine that can tolerate 1/3 of connected machines failing. A major quality of Tendermint is its fast finality - Once a block is processed, all transactions included in the block are considered finalized. There is no need to wait for confirmations like Proof-of-work chains.

On MakeOS, fast finality is important because it guarantees that when a push request is made, it will not be reversed. Developers do not have to wait beyond the first block to be certain that their push operation was successful. On a proof-of-work chain, the possibility of a block re-organization means that a push operation may be reversed, requiring developers to re-push.

MakeOS leverages on proof-of-stake to provide Sybil protection. It requires all nodes participating in block creation to lock funds that may be slashed when bad behaviour is detected.
