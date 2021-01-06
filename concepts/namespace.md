---
id: namespace
title: Namespace
sidebar_label: Namespace
---

# Namespace

## Overview

A namespace is a collection of user-readable identification names used to represent repositories and user accounts on the MakeOS network. 

A namespace is like an internet domain name in that it can be used to map a network resource whose identifier is not human-readable to a more user-friendly identifier.

### Syntax

`namespace/domain`

Where:

* `namespace`: is a network-wide unique identifier.
  * `domain`: is the name of an entry that points to a network resource.

## Namespace as an Organization

While a namespace core function is to map human-readable names to network resources, it can also be used to create a similar organization structure that exists on centralized code collaboration platforms.

A namespace can represent an organization that has many repositories and contributors.

It can also include access control rules for repositories under it such that when a repository is accessed via a namespace, the user will be subjected to access control policies configured on the namespace.

## Namespace Characteristics

* A namespace contains alphanumeric characters \(including underscore and hyphen\).
* Must be at least 3 characters long. 
* Contains one or more domain entries.
* Requires a fee to register. 
* Expires after 1 year + grace period.
* Can be owned by a user account or a repository. 

## Namespace Registration

Like internet domains, a namespace is leased by the network to a user for a fee. 

This lease will last for a year and must be renewed for another year if the lessee wants to retain control. 

Fees serve as a mechanism for discourage squatting. When a namespace reaches its expiry date, a grace period begins, giving the lessee a final chance to renew.

If the namespace is not renewed during the grace period, it is released to the market for repurchase. 

## Lease Fee

The price of a namespace will be determined by the length of the chosen name. Current implementation imposes a flat fee; This will change in future releases.

## Ownership

A namespace is first acquired by a user, after which it can be transferred to another user or a repository in the same transaction. 

When a namespace is transferred to a repository, the namespace becomes the asset of the repository and as such subject to its governance configuration.

## Domain

A domain is a key-value record in a namespace.

The key can be a human-readable identifier that points to a specific network resource. 

The key contains alphanumeric \(including underscore and hyphen\) characters and can have a length of not more than 128 characters.

Currently, a domain can point to a Balance Account address or a repository. 

## Target

A target is the identifier of the actual resource pointed to by a domain. A target can be an address of a Balance Account or a full repository name.

## Create a Namespace

Currently, you can create a namespace with domains that point to a user account or a repository.

### To Repository

The example below creates a namespace named `facebook` with a single domain named `react` that points to a repository named `r/react`. The `r/` prefix indicates that the target is a repository identifier.

```javascript
ns.register({
   name: "facebook", 
   value: "1", 
   fee: "0.01",  
   domains: {
      "react": "r/react"
   }
}, user.getKey(accounts[0], "passphrase"))
```

The repository can now be accessed using the full path `facebook/react`.

#### **Fields:**

* `name`: is the unique name of the namespace 
* `value`: is the registration fee to be paid. 
* `fee`: The network transaction fee. 
* `domains`: Contains domain and target pairs. 
* `to`: An optional Balance Account address or name of a repository that will own the namespace.

### Set Git Remote To Namespace Path

MakeOS remote nodes can resolve push/fetch requests to a namespace domain pointing to a repository. 

For example, you can set the remote URL of a repository to `https://remote.com/facebook/react`. When you push or pull, the remote server will resolve to the `r/react` repository.

### To User Account

The example below creates a namespace with a domain named `donate` that points to a Balance account with the address `a/os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u`. The `a/` prefix indicates that the target is a user account address.

```javascript
ns.register({
   name: "myproject", 
   value: "1", 
   fee: "0.01",  
   domains: {
      "donate": "a/os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u"
   }
}, user.getKey(accounts[0], "passphrase"))
```

A namespace URI `myproject/donate` can be used in place of the address `os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u` when providing the recipient of a coin transfer transaction.

