---
id: validator
title: Validator
sidebar_label: Validator
---

# Validator

MakeOS is a proof-of-stake blockchain built on top the Tendermint consensus engine. 

Tendermint is a fast BFT consensus engine that offers fast finality and block time. When a block is processed, all transactions in the block are considered confirmed and finalized. No need to wait for more blocks. 

Blocks are proposed, validated and executed by network participants known as _Validators_.

## Validator Stake

Unlike Proof-of-Work chains, Proof-of-Stake blockchains have a different security model where block producers lock up funds with the network to gain the right to create blocks and earn rewards. 

On PoW, security is derived from the computers solving hard mathematical puzzles that get harder perpetually. Miners compete by purchasing highly specialized hardware which also contributes to the security of the network. An attacker will have to outcompete the rest of the PoW network in other to harm the system. 

On PoS, instead of purchasing and using specialized hardware, validators lock up the equivalent amount of funds they would have used to purchase mining hardware. 

Validators with the largest amount of locked-up funds gain the power to create new blocks and earn a reward for advancing and protecting the network. 

On MakeOS, validators stake a minimum amount of the native coin \(“Latinum”\) to have a chance at producing blocks.

## Validator Tickets

MakeOS uses a ticket-based system for validator staking. 

Validators stake funds by purchasing tickets that get entered into a draw where some are randomly selected to be part a set of 100 validators that will produce blocks over a period of time. 

A validator ticket passes through a maturity period before it is eligible for selection and it has a limited lifespan — It will expire after a period of time has passed. 

Ticket owners may unbond their tickets and get their funds back. However, this process will take some time to complete. This waiting period is known as the _thawing_ period.

## Validator Reward

Validators earn a percentage of coins generated on every block they produce. They share the block reward with hosts, remotes and repositories.

## Delegation

Running and maintaining a validator node requires attention and technical skills. There will be many without these skills. 

The protocol supports a delegation system that will let users purchase tickets and delegate them to active Validators. 

Each time the validator produces a block, the reward allocated to it is shared between itself and its delegates in proportion to the value of their delegated stake.

## Dilithium Consumption

Validators require Dilithium to be able to mine blocks. Every transaction process incurs a fee known as a _protocol tax_. 

The protocol tax is paid to the protocol for the privilege to participate in the network and to create a demand-driver for Dilithium. 

The protocol will deduct and burn a validator’s dilithium whenever they process transactions in a block. 

If a validator does not have enough Dilithium to process a transaction, they will only receive a block reward proportional to the amount of Dilithium spent. 

If the validator consistently burns less Dilithium below a threshold, they will eventually be unbonded and removed as validators. 

## Dilithium Earning

Just as how validators burn Dilithium, they also earn some from users who pay for push operations with Dilithium.

