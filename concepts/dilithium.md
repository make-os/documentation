---
id: mining
title: Mining Dilithium
sidebar_label: Mining Dilithium
description: An energy currency for paying for low-level protocol fees.
---

# Dilithium

## Overview

The MakeOS protocol is built on the idea that everything requires energy and no value can be created without expending energy. 

On MakeOS, network participants require energy to do work that produces value. This energy requirement is similar to gas on Ethereum, except MakeOS gas is tangible, divisible, transferable and can be stored in an account. 

MakeOS quantifies and stores energy in a native token known as **Dilithium**. 

Dilithium serves as a currency for paying protocol fees — Protocol fee is a fee charged by the protocol for performing low-level network operations such as transaction execution, endorsements etc.  

For instance, a validator must actively maintain a Dilithium balance to continue to process new blocks and receive rewards since individual transactions will require an about of Dilithium to be burnt. 

## Dilithium Mining

Like Lithium mining in the real-world, _Dilithium_ is also mined but via Proof-of-Work — A process that involves solving hard mathematical computations to arrive at a target value that can be verified by the network. 

When Dilithium is mined, a proof is sent to the network for verification. If it is valid, the Dilithium balance is credited to the miner’s account.

## Dilithium Life Span

Unlike its companion currency \(“Latinum”\), Dilithium decays over time. 

This means it loses its balance over time until it gets to zero. 

If a miner does not use stored Dilithium after a period of time, it becomes depleted. 

Dilithium is destroyed when paid to the network as a fee for work done.

## Dilithium Shielding

Dilithium can be prevented from decaying through a process called "shielding". When a Dilithium is shielded, its decay property is paused. 

To shield Dilithium, an amount of Latinum must be staked in the network shield contract. For example,  a user who owns a Dilithium with charge balance of 10 may pause its decay by staking 20 Latinum.

Dilithium will not experience decay as long as a fixed amount of Latinum is bonded in the shield contract. The moment it is no longer bonded, it will continue to decay again. 

## Mining Participants

Dilithium is mined by:

* Git users who want to push without paying network fees in Latinum.
* Dedicated miners who mine the fixed amount of Dilithium over a given period.

## Dilithium Use Case

* Used by validators to process transactions.
* Used by endorsers to pay for endorsement processing. 
* Used by git users for paying push operation fees. 
* Used by repository owners to convert into repository currency.
* Used by Dilithium miners to vote out a validator or host. 

## Initial Supply

At genesis, the expected initial supply of dilithium will be about 2 600 000 000 \(2.6 Billion\). This supply will be seeded by miners who mined on the MakeOS cloud [mining service](https://mine.makeos.org).

{% hint style="warning" %}
**There is no cap on the number of Dilithium to be mined on the cloud mining platform.** The amount of Dilithium that will be used to seed the mainnet is dependent on: 

* How much Dilithium is left after the global Latinum conversion event ends.
* How much Dilithium was claimed. 
{% endhint %}



