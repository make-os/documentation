# Transactions

A transaction is a first-class concept in blockchain technology. It is the initiator of blockchain events that alter the state of the blockchain. 

When a transaction is sent to the network, included in a block and executed, it will alter the state of the blockchain.

## Types Of Transactions

MakeOS depends on a wide range of transaction types to perform its core functions. As at current development progress, the protocol supports transactions for:

{% hint style="warning" %}
**WIP:** The section is incomplete.
{% endhint %}

* [Sending funds between accounts and repositories.](send-fund.md)
* [Creating a repository.](register-repo.md)
* Registering a namespace.
* Updating a namespace.
* Push key registration.
* Creating repository proposals for:
  * Adding contributors to a repository.
  * Updating a repository.
  * Add or update owners to a repository
  * Updating the contributors of a repository.
* Contributing to a proposal’s deposit fee.
* Vote on a proposal\].
* Finalizing push operations.
* Setting the delegate commission rate. 
* Purchasing validator or host ticket.
* Un-bonding validator ticket.

## Transaction Fee

A transaction fee is a fee charged by the MakeOS protocol for validating and executing transactions in a block. Transaction fee serves as a mechanism for prioritizing transactions, incentivizing network participants involved in transaction processing and for discouraging spam.

MakeOS requires fees for most transactions. However, push transactions fees can be paid for using the native coin or Dilithium — Dilithium is the fuel used by every network participant to perform protocol operations. Dilithium is mined via Proof-of-work.

During a `git push` operation, a developer may choose to spend some time mining enough dilithium to pay the push fees or instruct the network to charge their native coin or dilithium balance if they cannot wait. Mining dilithium to pay for push fees essentially makes push operations free.

