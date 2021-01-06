---
id: access-control
title: Access Control
sidebar_label: Access Control
---

# Access Control Config

A MakeOS repository is open and accessible to everyone in the world. However, many users will need the ability to control who can perform actions on it. 

Maintainers will need the ability to grant privileges to contributors similarly to how they can do so on traditional code collaboration platforms. 

MakeOS allows owners of a repository to set policies that allow or deny access to perform certain operations. 

Like [governance configuration](config.md), policies can be added when creating a new repository or through a repository update proposal.

## What is a Policy

A policy is a rule that determines what action can be performed by an entity against a specific repository’s resource.

### A policy includes:

* a subject: A user or entity the policy targets.
* an object: The target resource the policy will be applied to.
* an action: The action that can be executed against the object by the subject.  

## Example

The policy below grants `write` action to the push key `pk1wfx7vp8qfy...xjrj48tpkfwme7`, allowing the contributor that controls the key to do a push request to the branch named `refs/heads/dev`.

```javascript
{ 
   "sub": "pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7",
   "obj": "refs/heads/dev",
   "act": "write"
}
```

## Policy Subject

A policy subject is an entity that is the target of one or more rules defined in a policy. The object can only interact with the repository based on the policies addressed to it. A subject can be one of the following:

* A push key address \(e.g `pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7`\).
* `creator`: The creator of the target object or resource.
* `contrib`: A contributor to the repository.
* `all`: Everyone on the network.

## Policy Object

A policy object is a repository resource that subject is allowed to or restricted from interacting with;  A policy specifically dictates how the subject can interact with the object. MakeOS allows branches, tags, notes or reference root path as subjects. The object can be:

* `refs/heads`: Branches under the `refs/heads` path will be captured.
* `refs/heads/branch`: Only a branch named `branch` is captured.
* `refs/tags`: All tags under `refs/tags`  path are captured.
* `refs/tags/v1.0`: Only a tag named `v1.0` is captured.
* `refs/notes`: All notes under `refs/notes`  path are captured.
* `refs/notes/intro`: Only a note named `intro` is captured.
* `refs/heads/issues`: All issues under `refs/heads/issues`  path are captured.
* `refs/heads/issues/1`: Only an issue with ID =  `1`  is captured.
* `refs/heads/merges`: All merge requests under `refs/heads/merges`  path are captured.
* `refs/heads/merges/1`: Only a merge request with ID =  `1`  will be captured.

## Policy Action

A policy action describes the action a subject is allowed to perform against a target object. MakeOS supports the following actions:

* `write`: Allows the subject to perform write operation \(e.g push\). 
* `deny-write`: Deny the subject the right to perform a write operation. 
* `update`: Allows the subject to perform write operations reserved for an admin.
* `deny-update`: Deny the subject the right to perform an admin write operation.
* `delete`: Allows the subject to perform delete operation.
* `delete-deny`: Deny the subject the right to perform delete operation.

## How to Add Policies

Here is how to set repository policies when creating a new repository:

{% tabs %}
{% tab title="CLI" %}
```bash
kit repo create "myrepo"  \
    --signing-key=0  \
    --fee=1.51  \
    --config='{ "policies": [{ 
        "sub": "all", 
        "obj": "refs/heads/master",
        "act": "deny-delete" }]}'
```
{% endtab %}

{% tab title="Console" %}
```javascript
repo.create({ 
   name: "myrepo", 
   fee: "0.01", 
   value: "10",
   config: {
      "policies": [{ "sub": "all", "obj": "refs/heads/master", "act": "deny-delete"}]
   }
}, user.getKey(accounts[0],"passphrase"))
```
{% endtab %}
{% endtabs %}

## Default Policies

MakeOS sets default policies for new repositories. You can override these policies by providing a non-empty `config` object when creating or updating your repository.

| Object | Subject | Action | Description |
| :--- | :--- | :--- | :--- |
| refs/heads/issues | all | write | Anyone can create an issue |
| refs/heads/merges | all | write | Anyone can create a merge request  |
| refs/heads | contrib | write | Only contributors can create branches |
| refs/heads | contrib | delete | Contributors can delete any branch |
| refs/heads/master | contrib | deny-delete | Contributors cannot delete `master` branch |
| refs/tags | contrib | write | Contributors can create tags |
| refs/tags | contrib | delete | Contributors can delete tags |
| refs/notes | contrib | write | Contributors can create notes |
| refs/notes | contrib | delete | Contributors can delete notes |
| refs/heads/issues | contrib | delete | Contributors can delete issues |
| refs/heads/issues | contrib | update | Contributors can update admin properties of an issue |
| refs/heads/issues | creator | delete | Issue creators can delete issues they created |
| refs/heads/issues | creator | update | Issue creators can update admin fields of the issues they created |
| refs/heads/merges | creator | delete | Merge request creators can delete merge requests they created |
| refs/heads/merges | creator | update | Merge request creators can update admin fields of requests they created |
| refs/heads/merges | contrib | update | Contributors can update admin fields of a merge request |
| refs/heads/merges | contrib | delete | Contributors can delete merge requests |

