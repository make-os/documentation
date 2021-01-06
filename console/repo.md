---
id: repo
title: Repository Module
sidebar_label: Repository
---

# repo

This module allows you to create and manage a MakeOS repository. It can be accessed from the global variable `repo`.

## create

```javascript
repo.create(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Send a transaction to create a repository.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `name` - `String` : The unique name of the repository.
   * `value` - `String`:  \(optional\) The amount of coins to transfer to the new repository.
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The Unix timestamp of the transaction.
   * `config` - `Object`: \(optional\) The repository configuration
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key to use to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.
* `address` - `String`: The full address of the repository.

### Example

* Create a transaction to create a repository named `myrepo`.
  * `accounts[0]` returns the address of a key at index 0 on the keystore. 
  * You will be prompted to enter the passphrase.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
repo.create({ 
   name: "myrepo", 
   fee: "0.1", 
   value: "15.5"
}, user.getKey(accounts[0]))
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
  "address": "r/myrepo",
  "hash": "0x59e77af29938528284b69f8114a3ece38493e83725c3354ed840e2b8c86b39e3"
}
```
{% endtab %}
{% endtabs %}

* Get the signed payload instead of creating and then sending the transaction. 

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var payload = repo.create({ 
   name: "myrepo", 
   fee: "0.1", 
   value: "15.5"
}, user.getKey(accounts[0]), true)
```
{% endtab %}

{% tab title="Output" %}
```bash
{
  "config": {},
  "fee": "1",
  "name": "myrepo",
  "nonce": 1,
  "senderPubKey": [121,172,241,123,81,102,72,134,112,163,3,245,128,196,144,219,42,147,70,184,226,63,26,28,135,151,128,139,16,82,174,4],
  "sig": [184,29,52,29,244,75,118,183,214,245,205,15,170,131,69,60,15,110,172,211,11,122,96,199,175,70,5,79,127,189,23,199,13,87,77,37,8,219,206,101,109,82,123,150,202,101,78,142,22,202,46,1,165,25,229,31,112,102,58,184,121,20,221,3],
  "timestamp": 1606173977,
  "type": 6,
  "value": "0"
}
```
{% endtab %}
{% endtabs %}

## upsertOwner

```javascript
repo.upsertOwner(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Create a proposal to add or update an owner of a repository.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `id` - `String`: A unique, numeric proposal ID. Must not exceed 16 characters.
   * `name` - `String` : The unique name of the repository.
   * `value` - `String`:  \(optional\) The proposal deposit fee, if required.
   * `addresses` - `Array<String>`: A list of addresses to add as owners.
   * `veto` - `Boolean`: Grant veto right to owners.
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The unix timestamp of the transaction.
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key to use to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

* Create a transaction that adds a new address as an owner with veto power.

```javascript
repo.upsertOwner({
   id: "1",
   name:"myrepo", 
   veto: true, 
   addresses: ["os1858effdlfecl30hgq0dvpesygp2daf97malemz"], 
   fee: "1", 
}, user.getKey(accounts[0]))
```

## vote

```javascript
repo.vote(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Create a transaction that votes on a repository proposal.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `id` - `String`: The ID of the proposal.
   * `name` - `String` : The name of the repository.
   * `vote` - `Number`:  The vote choice: 
     * 0: `No`, 
     * 1: `Yes`
     * 2: `NoWithVeto`
     * 3: `Abstain`
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The Unix timestamp of the transaction.
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key to use to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

* Create a transaction that will vote `Yes` on a proposal with ID = `1`.

```javascript
repo.vote({ 
   name: "myrepo", 
   id: "1", 
   vote: 1, 
   fee: "1" 
}, user.getKey(accounts[0]))
```

## get

```javascript
repo.get(name, queryopts)
```

Create a transaction that votes on a repository proposal.

### Parameters

1. `name` - `String`: The name of the repository.
2. `queryopts` - `Object`: **The query options**
   * `height` - `Number|String`: \(Optional\) The chain height to search for repository. Defaults to the latest block height.
   * `noProps` - `Boolean` : If true, proposals will not be returned. 

     **Returns**

     `Object` - **The result object**
3. `balance` - `String`: The coin balance of the repository.
4. `config` - `RepoConfig`: The repository configuration.
5. `contributors` - `{PushKey: [RepoContributor](#)}`: The repository contributors.
6. `owners` - `{Address: [RepoOwner](#)}` - The owners of the repository.
7. `proposals` - `{ID: [RepoProposal](#)}` - The proposals created on the repository.
8. `references` - `{Reference: [RepoReference](#)}` - The git references of the repository.

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
repo.get("myrepo")
```
{% endtab %}

{% tab title="Origin" %}
```javascript
{
  "balance": "0",
  "config": {RepoConfig},
  "contributors": {"pk1..": RepoContributor},
  "owners": {"os1..": RepoOwner},
  "proposals": {"1": RepoProposal},
  "references": {"refs/heads/master": RepoReference}
}
```
{% endtab %}
{% endtabs %}

## update

```javascript
repo.update(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Create a proposal to update a repository.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `id` - `String`: A unique, numeric proposal ID. Must not exceed 16 characters.
   * `name` - `String` : The unique name of the repository.
   * `value` - `String`:  \(optional\) The proposal deposit fee, if required.
   * `config` - `Object`: The config update to merge into the existing configuration.
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The Unix timestamp of the transaction.
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key to use to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

```javascript
repo.update({ 
   name: "myrepo", 
   id: "1", 
   fee: "1", 
   config: {
      governance: { propQuorum: 35 }
   }
}, user.getKey(accounts[0]))
```

## depositPropFee

```javascript
repo.depositPropFee(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Creates a transaction that deposits the native coins to pay the proposal fee. Anyone can create this transaction. Depending on the repository's proposal fee configuration, the proposal fee may be returned after the proposal is finalized.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `id` - `String`: A target proposal ID that will receive the deposit.
   * `name` - `String` : The unique name of the repository.
   * `value` - `String`:  The amount to deposit as proposal fee. 
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The unix timestamp of the transaction.
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key to use to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

* Create a transaction that will deposit 50 coins to a proposal with ID = `1`.

```javascript
repo.depositPropFee({ 
   id: "1",
   name: "myrepo", 
   fee: "1", 
   value: "50",  
}, user.getKey(accounts[0],"marvel"))
```

## addContributor

```javascript
repo.addContributor(txObject, [signingKey | payloadOnly | [signingKey, payloadOnly]])
```

Creates a proposal that adds contributors to a repository.

### Parameters

1. `txObject` - `Object`: **The transaction object**
   * `id` - `String`: A unique, numeric proposal ID. Must not exceed 16 characters.
   * `name` - `String` : The unique name of the repository.
   * `value` - `String`:  \(optional\) The proposal deposit fee, if required.
   * `keys` - `Array<String>`: A list of push keys to add as contributors
   * `policies` - `Array<[ContributorPolicy](#)>`: A list of access policies to apply to the contributors.
     * `feeMode` - `Number`: The fee mode determines who pays the fees whenever a contributor performs a push operation. There are 3 fee mode options: 
       * 0: Contributor pays for their fees.
       * 1: Repository pays for contributors fees. 
       * 2: Repository pays a capped amount of contributors fees. 
   * `feeCap` - `Number`: The maximum amount of fees payable by the repository if `feeMode` is `2`.
   * `namespace` - `String`: Adds the push keys as namespace-level contributors. Note: The repository must own the namespace.
   * `namespaceOnly` - `String`: Adds the push keys only as namespace-level contributors. They will not be added as contributors to the repository itself. Note: The repository must own the namespace. 
   * `nonce` - `Number|String` : The signing account’s next nonce. 
   * `fee` - `String`: The network fee to be paid by the signing account. 
   * `timestamp` - `String`: \(optional\) The unix timestamp of the transaction.
   * `sig` - `String` : \(optional\) The transaction signature. If not provided, the transaction will be signed using the `signingKey`.
2. `signingKey` - `String`: \(optional\) The private key to use to sign the transaction. 
3. `payloadOnly` - `Boolean`: \(optional\) When true, the transaction payload is returned instead of being sent to the network.

### Returns

`Object` - **The result object**

* `hash` - `String`: A 32 bytes transaction hash.

### Example

```javascript
repo.addContributor({
   id: "1", 
   name: "myrepo",
   keys: ["pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7"],  
   fee: "1"
}, user.getKey(accounts[0]))
```

## track

```javascript
repo.track(names, [height])
```

Track one or more repositories. If a repository is added to the tracklist, only the repository's push updates will be synchronized and stored on the node. You can track as many repositories as you want.

### Parameters

1. `names` - `String`: A comma separated list of repository names.
2. `height` - `String|Number`: \(Optional\) The block height to begin synchronization from. 

### Examples

* Track a repo named `my_repo`.

```javascript
repo.track('my_repo')
```

* Track repositories named `my_repo` and `someones_repo`

```text
repo.track('my_repo,someones_repo')
```

## untrack

```javascript
repo.untrack(names)
```

Untrack one or more repositories.

### Parameters

1. `names` - `String`: A comma-separated list of repository names.

### Examples

* Untrack a repo named `my_repo`.

```javascript
repo.untrack('my_repo')
```

* Untrack repositories named `my_repo` and `someones_repo`.

```javascript
repo.untrack('my_repo,someones_repo')
```

## tracked

```javascript
repo.tracked()
```

Get all tracked repositories.

### Returns

`Object` - **The result object**

```typescript
interface Result {
    [repoName: String]: {updatedAt: String} 
}
```

### Example

{% tabs %}
{% tab title="JavaScript" %}
```javascript
repo.tracked()
```
{% endtab %}

{% tab title="Output" %}
```javascript
{
  "my-repo": {
    "updatedAt": "1005"
  }
}
```
{% endtab %}
{% endtabs %}

