---
id: merge-request
title: Merge Request
sidebar_label: Merge Request
description: >-
  A protocol that allows users to request to merge changes into a restricted
  branch of a repository.
---

# Merge Request

The ability to request a branch to be merged into another branch is invaluable to collaborators today. It allows collaborators to propose changes to source code, have it reviewed and finally merged into a primary base. On this page, you will learn:

* About merge request proposal
* How the merge request works.
* Create a merge request.
* Add comments to a merge request.
* Close and reopen a merge request.
* List merge requests. 
* Check the status of a merge request branch.

## Overview

Like issue management, a merge request \(also known as Pull Request\) is a feature that developers on centralized code sharing and collaboration platforms have come to heavily depend on to coordinate and review changes to a codebase. 

Many developers have built their workflow around this feature which makes it mandatory for any code collaboration alternative to support such workflows without changing much of the user experience.

MakeOS includes a merge request protocol built on top of git. The protocol allows developers to create merge requests right inside a local repository.

## Merge Request Proposal

On MakeOS, a proposal is a type of transaction that seeks to change one or more properties of a resource managed by a repository. 

Proposals allow stakeholders of a repository to propose changes and also vote on the acceptance of proposed changes. 

A merge request is a kind of proposal that proposes changes to a given base branch. 

## Merge Request Branch

MakeOS merge requests are offline-first. This means they first exist locally in a branch called `merges`. 

Like regular branch workflow, a developer can create a merge request locally and push them to the network whenever they are ready. 

Merge requests branches exist under the branch `merges` and are numerically named \(e.g `/refs/heads/mr/1`\). 

Like an issue branch, a merge request branch contains a single file named `body` which contains a front matter and body sections. The front matter part is used to store merge request metadata while the body section contains the content describing the merge request.

## How Merge Request Works

To create a merge request: 

1. Create a merge request branch; Provide the following: 
   * Title 
   * Body
   * Base branch name. 
   * Base branch hash. 
   * Target/Source branch name. 
   * Target/Source branch hash. 
     * Note: _Base and target branches must have been pushed to the network before creating a merge request._ 
2. Push the merge request branch. 
3. On a successful push, a merge request proposal will be created. 
4. Depending on the governance configuration of the repo, the merge request proposal might need to be voted on and accepted by members before the target branch an be merged into the base branch. By default, a proposal is automatically accepted if it has only one owner.
5. On successful approval, the target branch can be pushed to the remote base branch with the merge proposal ID in the request. 
6. The push is accepted if the proposal target branch and the pushed branch match.

## **How to Create a Merge Request** <a id="check-out-the-base-branch"></a>

### **Step 1: Check out the base branch**

Check out the base branch you want to merge your changes into. Here we are using a branch named `master`

```bash
git checkout master
```

#### Push the base branch

{% hint style="info" %}
We are using`origin`as our remote name since our network remote node was added under the `origin` name. 
{% endhint %}

To create a valid merge request, the base branch must exist on the network. We need to push the branch to the network.

```text
git push origin master
```

### Step 2: Create a feature branch

{% hint style="warning" %}
The feature branch must be a fork of the base branch to allow git to use the fast-forward merge strategy when merging back the base branch. If the feature branch is not a fork of the base branch, the merge request will fail protocol validation.
{% endhint %}

From the base branch, create a new branch that will contain your updates. For example, we will create a feature branch named `feat` that will add a new file named `file.txt`. 

```bash
git checkout -b feat              # create new branch
touch file.txt                    # add a new file
```

#### Push the feature branch

{% hint style="info" %}
We are using`origin`as our remote name since our network remote node was added under the `origin` name. 
{% endhint %}

Now that we have a feature branch with some changes, we must push the feature branch to the network. 

```bash
git push origin feat
```

### Step 3: Create a merge request

The next step is to create the merge request; The `kit mr create` command is used to create the merge request. First, we may check out the base branch:

```bash
git checkout master
```

Then create the merge request: 

{% tabs %}
{% tab title="Bash" %}
```bash
kit mr create --target="feat" --targetHash="~"
```
{% endtab %}

{% tab title="Output" %}
```
Title> Add Comment Section
Body> I have added a comment section for users...
✅ New merge request created!
refs/heads/merges/1#0
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
As seen in the output tab above, you will be asked to provide a title and body. 
{% endhint %}

This will create a merge request branch named `merges/1`, where `1`  is the merge request unique identifier. You can specify an alternative number by using the `-i` flag.

`--target` flag species the target branch that will be merged into the base branch `master`. For us, the `feat` branch is our target branch. 

`--targetHash` flag specifies the hash we expect the base branch to change to after a successful merge. We used `~` to indicate that we want the current hash of the`target`branch but you can explicitly provide the full hash if you wish.

{% hint style="info" %}
If the target branch is on a different repository, set target using the format `/<repo-name>/<branch>`. For example, if the target branch `dev` exists on a repo named`example`, the `--target` will be `/example/dev`. If`--target` is not prefixed with `/` it will be considered as a branch on the base repository.
{% endhint %}

#### **Push merge request**

Since a merge request is just a special branch, it needs to be pushed to the network where it will be used to create a merge request proposal. 

```bash
git push origin merges/1
```

### Step 4: Merge feature branch into the base branch

It is time to merge the feature branch into the base branch such that the base branch and the feature branch become the same.

If the base branch has not been updated since the feature branch created from it, there will be no merge conflict.

{% tabs %}
{% tab title="Bash" %}
```bash
git merge feat
```
{% endtab %}

{% tab title="Output" %}
```bash
Updating f6dd022..5410769
Fast-forward
 file | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```
{% endtab %}
{% endtabs %}

{% hint style="danger" %}
If there is a merge conflict, it means the base branch’s new hash \(after the merge conflict is resolved\) will not match the merge request target hash and as such the merge request cannot be fulfiled.
{% endhint %}

### **Step 5: Push the base branch \(fulfilment\)**

After the proposal created in [Step 3](merge-request.md#create-a-merge-request-1) is accepted, the base branch can now be pushed to the network to fulfil the merge request. 

```bash
git config sign.mergeID "1"
git push origin master
```

Line 1 sets the merge request ID `1` for which the push operation intends to fulfil.  It tells the network that the intent is to fulfil a merge the new changes of the base branch according to match the approved target of a merge request with `ID=1`. 

## Add a Comment

Every commit in a merge request branch represents a comment or a response to another comment in the merge request branch. You can add a comment by specifying the target merge request using the `-i` flag.

{% tabs %}
{% tab title="Bash" %}
```bash
kit mr create -i=1 
```
{% endtab %}

{% tab title="Output" %}
```bash
Body> We may need to re-think init sequence...
✅ New comment added!
refs/heads/merges/1#1
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
`-i` flag is not required if you are already checked into the target merge request branch.
{% endhint %}

## Add a Reply

Similar to comments, a reply is a comment that references the hash of another comment \(a commit\) in the same branch. You can add a comment by providing the target commit hash using `--reply` or `-r` flags.

{% tabs %}
{% tab title="Bash" %}
```bash
kit mr create -i=1 --reply="0f67159cea65546...c861289160f"
```
{% endtab %}

{% tab title="Output" %}
```bash
Body> Can we try to recreate the problem by...
✅ New comment added!
refs/heads/merges/1#2
```
{% endtab %}
{% endtabs %}

## Add a Reaction

A reply can also include reactions to the comment being responded to. MakeOS supports the [v13.0](http://www.unicode.org/emoji/charts/emoji-list.html) emoji list, allowing collaborators to express themselves however they wish. 

Add reactions using the `--reactions` or `-e` flags.

```bash
kit mr create -i=1 --reply="0f67159cea65546...c861289160f" -e="smiling_face,sparkle"
```

## List All Merge Requests

List all merge requests in the repository with `list` command: 

{% tabs %}
{% tab title="Bash" %}
```bash
kit mr list
```
{% endtab %}

{% tab title="Output" %}
```
merge-request eb2341fc3d36498860a6ebfd10513f481983a66d merges/20
Title:          Added Footer
Base Branch:    master
Base Hash:      d43c6e3a78...888547b634a
Target Branch:  feat
Target Hash:    f36650d17f...eefdf1d0ff4
Author:         John email@example.com
Pusher:         pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7
Date:           Wed Aug 12 15:06:10 2020 +0100
    
    Added the missing footer to the page.html...
    
merge-request gysgfjfysgri384h8494hsg830jgkshs7495fhsg merges/19
Title:          Added Header
Base Branch:    master
Base Hash:      dh48shf94h...h58sg49fjsh
Target Branch:  feat
Target Hash:    hdurihe94d...jgjt94jdbsb
Author:         John email@example.com
Pusher:         pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7
Date:           Wed Aug 13 11:12:10 2020 +0100
    
    Adds a responsive header component to...
```
{% endtab %}
{% endtabs %}

The command above will list all merge requests ordered by their commit date in descending order. Use `--reverse` to reverse the order. You can also limit the number of issues returned with `--limit` or `-n` flags. 

## Read a Merge Request

Use `read` command to read the comments of a specific merge request. Supposing there is a merge request with ID = `2`, it can be read like this:

{% tabs %}
{% tab title="Bash" %}
```bash
kit mr read 2
```
{% endtab %}

{% tab title="Output" %}
```
merge-request eb2341fc3d36498860a6ebfd10513f481983a66d merges/2
Title:          Added Footer
Base Branch:    master
Base Hash:      d43c6e3a78...888547b634a
Target Branch:  feat
Target Hash:    f36650d17f...eefdf1d0ff4
Author:         John <email@example.com>
Pusher:         pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7
Date:           Wed Aug 12 15:06:10 2020 +0100
```
{% endtab %}
{% endtabs %}

Like the list command, it will list all comments ordered by their commit date in descending order. Use `--reverse` to reverse the order. You can also limit the number of comments returned with `--limit` or `-n` flags.

## Close a Merge Request

Close a merge request with the `close` command. The example command below will close a merge request with ID=`2`.

```text
kit mr close 2
```

Once a merge request has been closed and pushed to remote, new comments will not be accepted unless the comment includes a directive to re-opened the merge request.

## Re-open a Merge Request

To reopen a closed merge request, use `reopen` command:

```text
kit mr reopen 2
```

It creates a new comment that includes a directive in the front matter instructing the network to update the merge request state to “open”.

### Check Merge Request Status

```text
kit mr status 2
```

The command returns `opened` or `closed`.

