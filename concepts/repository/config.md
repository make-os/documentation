---
id: config
title: Configuration
sidebar_label: Configuration
description: Set up a repository's ownership and governance settings.
---

# Repository Governance

MakeOS offers repository owners or maintainers the ability to configure the ownership, governance and access control settings of a repository at creation time or through an approval vote system.

## Proposals

A proposal is a mechanism by which a repository's properties and assets are updated. 

To update a repository, a proposal describing the new changes must be submitted to the network and voted on by the repositories stakeholders.

The update will only take effect when the proposal is approved by a majority of the stakeholders.

MakeOS proposal system allows repository stakeholders to determine:

* What the majority is.
* Who can be classified as a stakeholder. 
* How long a proposal can last.
* If a fee is required for proposal creation as a way to limit low-quality proposals.

## Set Governance Config

A repository's governance properties can be set at creation time. It can also be set via a proposal after the repository have already been created.

### At Creation Time

Here is how to set the governance properties of a repository creation time:

{% tabs %}
{% tab title="CLI" %}
```bash
kit repo create 'myrepo'  \
    --signing-key=0  --fee=1.51  \
    --config='{ governance: {... add properties here ...}}'
```
{% endtab %}

{% tab title="Console" %}
```bash
repo.create({ 
   name: "myrepo", 
   fee: "0.01", 
   value: "10",
   config: {
      governance: {
         // ... add properties here ...
      } 
   }
}, user.getKey(accounts[0],"passphrase"))
```
{% endtab %}
{% endtabs %}

In the examples above, the repository governance config is a JSON structure that contains various config properties. The next section describes the various governance properties.

## Governance Configuration

These are the properties used to configure repositories:

## propVoter

**Type:** Integer

#### **Description:**

Set who can vote for or against proposals.

**Options:**

| **Value** | Description |
| :--- | :--- |
| 1 | Only repository owners can vote |
| 2 | Only users who own validator or host tickets. |
| 3 | Only network stakeholders and repository owners.  |

## propCreator

**Type:** Integer

**Description:**

Set who can create a proposal.

**Options:**

| **Value** | Description |
| :--- | :--- |
| 1 | Anyone can create a proposal**.** |
| 2 | Only a repository owner can create a proposal. |

## propDur

**Type:** Integer

**Description:**

Set the lifespan of proposals. For example, a duration of 100, means voting ends after 100 blocks has been processed since the proposal was created.

## propFee

**Type:** Float64

**Description:**

Set an amount a proposal creator must deposit in other to create a proposal. This can be used to discourage proposal spam. If `propFeeDepDur` is not provided, the whole fee must be paid in the proposal creating transaction.

## propFeeDepDur

**Type:** Integer

**Description:**

Set a duration within which proposal fees can be paid by anyone. If the duration is reached without all proposal fees deposited, the proposal’s will not reach the voting period and will be finalized as `InsufficientDeposit`.

## propQuorum

**Type:** Float64

**Description:**

Set the percentage of eligible voters that must vote. If this percentage is not reached by the end of the voting period, the proposal outcome is set to `QuorumNotMet`.

## propVetoQuorum

**Type:** Float64

**Description:**

Set the percentage of owners with veto powers that must vote `NoWithVeto` to veto a decision. If a proposal is rejected with a veto, the outcome is set to `RejectedWithVeto`.

## propVetoOwnersQuorum

**Type:** Float64

**Description:**

Set the percentage of owners with veto powers that must vote `NoWithVeto` to veto a proposal where network stakeholders are eligible voters. If a proposal is rejected with a veto, the outcome is set to `RejectedWithVetoByOwners`. For example, this property is useful for repositories that want to gradually cede control to the community but do not think the community is fully ready or mature.

## propThreshold

**Type:** Float64

**Description:**

Set the percentage of voters that need to vote in favour of the proposal `Yes` for it to pass.

## propFeeRefundType

**Type:** Integer

**Description:**

Determines how to handle refunds when a proposal did not pass.

**Options:**

| **Value** | Description |
| :--- | :--- |
| 1 | Fee will not be refunded no matter the outcome. |
| 2 | Fee is refunded if the proposal was accepted. |
| 3 | Fee is refunded if the proposal was accepted or rejected via `No` votes. |
| 4 | Fee is refunded if the proposal was accepted or rejected via `No` and `NoWithVeto` votes. |
| 5 | Fee is refunded if the proposal failed due to low voter threshold. |
| 6 | Fee is refunded if the proposal is accepted or it failed due to low voter threshold. |
| 7 | Fee is refunded if the proposal is accepted, rejected via `No` votes or it failed due to low voter. |
| 8 | Fee is refunded if the proposal is accepted, rejected via  `No` and `NoWithVeto` votes or it failed due to low voter threshold. |

## propTallyMethod

**Type:** Integer

**Description:**

Determines how votes are counted and weighted.

**Options:**

| **Value** | Description |
| :--- | :--- |
| 1 | For repositories where only owners can vote, each vote is counted as a single \(1\) vote power. |
| 2 | For repositories where only owners can vote, the available native coin balance of an owner is counted as their vote power. |
| 3 | Vote power is the total number of non-decayed tickets owned or delegated to a voter.  |
| 4 | Vote power is the total number of non-decayed tickets owned or delegated to a voter. Delegators may override a delegate's vote, thereby reducing the delegate’s vote power. |
| 5 | Vote power is the total number of non-decayed, non-delegated tickets owned by a voter. |
| 6 | Vote power is the total number of non-decayed, delegated tickets owned by a voter. |

## usePowerAge

**Type:** Boolean

**Default:** false

**Description:**

Determine whether to set the power age to the height of the block the proposal was processed in. If set to true, only owners that joined a repository before the proposal are allowed to vote. For stakeholders, only stakeholders with tickets that reached maturity at the time the proposal was created are allowed to vote.

## creatorAsContrib

**Type:** Boolean

**Default:** true

**Description:**

Determine whether to add the creator of the repository as the first contributor of the repository.

## noPropFeeForMergeReq

**Type:** Boolean

**Default:** true

**Description:**

Determine whether to disable proposal fees for merge request proposals. If it is set to false, a merge request will require a proposal fee to be paid if the repository’s `propFee` is &gt; 0.

