---
id: validator
title: Validator
sidebar_label: Validator
---

# Validator

MakeOS is a proof-of-stake blockchain built on top the Tendermint consensus engine.&#x20;

Tendermint is a fast BFT consensus engine that offers fast finality and block time. When a block is processed, all transactions in the block are considered confirmed and finalized. No need to wait for more blocks.&#x20;

Blocks are proposed, validated and executed by network participants known as _Validators_.

## Validator Stake

Unlike Proof-of-Work chains, Proof-of-Stake blockchains have a different security model where block producers lock up funds with the network to gain the right to create blocks and earn rewards.&#x20;

On PoW, security is derived from the computers solving hard mathematical puzzles that get harder perpetually. Miners compete by purchasing highly specialized hardware which also contributes to the security of the network. An attacker will have to outcompete the rest of the PoW network in other to harm the system.&#x20;

On PoS, instead of purchasing and using specialized hardware, validators lock up the equivalent amount of funds they would have used to purchase mining hardware.&#x20;

Validators with the largest amount of locked-up funds gain the power to create new blocks and earn a reward for advancing and protecting the network.&#x20;

On MakeOS, validators stake a minimum amount of the native coin (“Latinum”) to have a chance at producing blocks.

## Validator Tickets

MakeOS uses a ticket-based system for validator staking.&#x20;

Validators stake funds by purchasing tickets that get entered into a draw where some are randomly selected to be part a set of 100 validators that will produce blocks over a period of time.&#x20;

A validator ticket passes through a maturity period before it is eligible for selection and it has a limited lifespan — It will expire after a period of time has passed.&#x20;

Ticket owners may unbond their tickets and get their funds back. However, this process will take some time to complete. This waiting period is known as the _thawing_ period.

## Validator Reward

Validators earn a percentage of coins generated on every block they produce. They share the block reward with hosts, remotes and repositories.

## Delegation

Running and maintaining a validator node requires attention and technical skills. There will be many without these skills.&#x20;

The protocol supports a delegation system that will let users purchase tickets and delegate them to active Validators.&#x20;

Each time the validator produces a block, the reward allocated to it is shared between itself and its delegates in proportion to the value of their delegated stake.

