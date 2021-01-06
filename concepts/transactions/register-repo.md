---
id: register-repo
title: Create Repository
sidebar_label: Create Repository
---

# Register a Repository

Before you can start pushing, you must create a repository on the network and configure it. MakeOS allows you to use human-readable names as a repository identifier, configure governance, ownership and access policies.

In the examples below, we are creating a repository named `cashmap` and transferring `200` coins into its balance account.  A repository's balance account allows it to pay contributors network fee or for any other economic needs.

The repository’s initial configurations can be provided to `config`. See the [Repository Configuration](../repository/config.md) section for more details.

### Example

{% tabs %}
{% tab title="CLI" %}
```bash
kit repo create "cashmap" --signing-key=0 --fee="0.1"
```
{% endtab %}

{% tab title="Console" %}
```javascript
var alicePrivateKey = user.getKey(accounts[0], "pass&phrase")
repo.create({
   name: "cashmap",
   config: {},                // optional
   fee: "1", 
   value: "200",              // optional
   nonce: 3,                  // optional
}, alicePrivateKey)
```
{% endtab %}
{% endtabs %}

