---
id: host
title: Host (Replication)
sidebar_label: Host (Replication)
description: The storage and bandwidth provider of the MakeOS network.
---

# Host

## Overview

MakeOS provides a distributed hash table \(DHT\) network made up of nodes that offer git storage and retrieval services. 

Any node on the network can query for a specific git object and request for the object to be streamed to their machine. 

Nodes help replicate repositories that they care about by tracking them, fetching their updates and announcing to the network their ability to act as seed nodes.

## Repository Availability Concerns

In a p2p code collaboration, the availability of a repository is determined by how many nodes are actively tracking and seeding it. 

If a repository is popular, there will be many computers across the network tracking, fetching its updates and acting as seeds. However, if a repository is new and not popular, its content may only exist on its creator’s machine and may not be reachable from the internet due to ISP firewalls or a lack of networking skills. 

Due to this issue, owners of new or unpopular repository must actively seed their repositories until such a time when more users fetch and seed the repositories.  

One of the defining qualities of centralized collaboration platforms is the accessibility of all repositories regardless of their popularity. Without censorship, a new repository has the same accessibility level as an old or popular repository. This quality is one of the primary reasons open source continues to thrive. Developers are able to collaborate asynchronously and don't ever need to manage their own git servers. 

If a decentralized alternative wants to be accepted, it must find a way to replicate similar user-experience and benefits while also integrate the best qualities of decentralization. It cannot take users back to a time where they need to worry about setting up servers, maintaining uptime, waiting for fellow collaborators to fetch from their servers before they go on breaks. 

MakeOS solves the availability problem via network participants known as _Hosts._

## Host

MakeOS solves the availability problem by introducing a protocol participant known as a Host. They are git storage nodes responsible for:

* Storing git objects permanently.
* Endorsing push request received from remote servers.
* Act as relay nodes for users who cannot be reached from the public internet.

They are the archivers and endorsers of the network tasked with the responsibility of ensuring that immutability of all repositories is maintained.

Hosts collectively participate in git push operation processing pipeline by endorsing valid push operations. No Host will accept a push request unless a majority of hosts validate and approve the request.

Validators depend on hosts to assert that push operations are compatible and conflict-free. A validator will not process a push transaction found in a block if was not endorsed by the Hosts. 

To ensure a Hosts has access to git object, they will be periodically challenged via a Proof of Access protocol. A Host's bonded stake will be slashed if it is found to not have access to an object. 

Hosts are incentivized through inflation to perform these functions. They get a fraction of the block rewards. 

### Host Enrollment

Anyone can run the Kit client in host mode. 

However, to become a network-incentivized host capable of providing storage infrastructure for thousands of users, a minimum amount of Latinum must be bonded on the network. 

Hosts will randomly be challenged to prove that they have access to repositories and will have their deposit slashed if they fail the challenge.

### Delegation

Most people would be unable to provide the infrastructure required to participate as a Host. For this reason, the protocol allows anyone to delegate Latinum to any Host of their choice. 

The host may choose to share the network rewards it receives with the delegators. 

{% hint style="info" %}
Validators and Hosts can accept delegate stake. They can set the reward sharing formula by setting a commission rate on their validator account. For example, a Host that set their commission rate at 10% will keep only 90% of the block reward and share 10% with delegators in proportion to their stake. 
{% endhint %}

## Dilithium Consumption

{% hint style="info" %}
All low-level protocol participants \(e.g Validators, Host, Remotes\) spend Dilithium to perform protocol actions. They are the primary demand drivers of the Dilithium economy. 
{% endhint %}

Hosts spend Dilithium to create endorsements. 

When a Host sends out an endorsement, it will be considered invalid if the host does not have enough Dilithium balance to create the endorsement.

## Incentives

The host role is incentivized through network inflation and fees from push operations. Whenever a new block is produced, a fraction is allocated to the top Hosts. Hosts earn Dilithium from push transactions paid for with Dilithium.

