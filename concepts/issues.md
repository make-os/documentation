---
id: issues
title: Issues
sidebar_label: Issues
description: 'Create, read, list, react and close issue.'
---

# Issue Management

In this section, you will learn how to:

* Create an issue.
* List issues.
* Read an issue.
* Close and Open an issue

### Overview

Git is great. It was built to be very modular and as such does not come with many of the collaboration primitives we use today. One of which is a protocol for issue management. 

Issue management is an essential part of developers day-to-day activity. Developers rely on issue management systems to track and discuss problems they find in their codebase or those of projects they care about.

It is also a major driver of platform lock-in on centralized code sharing platforms. On these platforms, there are no issue management standards or a federated protocol for managing issues. Collaborators cannot simply and freely download and move their data to another platform in a way that is easy and compatible with the destination platform. 

MakeOS includes an issue management protocol built right into a repository using already existing git protocol. It is offline-first and anyone can build visualization and interactive tools on top of it.  

## Issue Branch

An issue is represented by a branch under the special`issues`directory. An issue branch must contain only a file named`post`which contains a frontmatter section \(for storing metadata\) and a body section. Adding a comment to an issue branch is as simple as updating the`post`file and committing it.

## Create Issue

Use the command below to create an issue:

{% tabs %}
{% tab title="Bash" %}
```bash
kit issue create
```
{% endtab %}

{% tab title="Output" %}
```
Title> My issue title
Body> I was trying to initialize the adapter...
✅ New issue created!
refs/heads/issues/1#0
```
{% endtab %}
{% endtabs %}

The command above will start an interactive session that will ask for a `title` and `body` of the issue. 

On success, it will create an issue branch at `.git/heads/issues/1`. 

Issues must have a numeric ID; The Kit client will create issues with a monotonically increasing number as the name. You can use `-i` flag to specify a different numerical number or to add a comment to an existing issue.  

#### Use an Editor

Writing a multi-line issue body on the terminal can be inconvenient. Use the`--use-editor`flag to launch an editor. 

The default editor is sourced from git's config option `core.editor`. You can provide an editor of your choice by changing the value of`core.editor`or using the`--editor`flag.

## Add Labels

The issue can include labels and assignees. Add up to 10 labels using `--labels` flag.

```bash
kit issue create --labels="bug,help-wanted"
```

## Add Assignees

Add up to 10 push keys as assignees. 

```bash
kit issue create --assignees="pk1e29gepyt8pzumrzjt9t508elgxpy62drezeect,pk1caskzq6leplwcj2su4jtsyu4w3fzutvl44hfn7"
```

## Add a Comment

Every commit in an issue branch represents a comment or a response to another commit \(or comment\) in the same branch. You can add a comment by specifying the target issue ID using the `-i` flag.

{% tabs %}
{% tab title="Bash" %}
```bash
kit issue create -i=1 
```
{% endtab %}

{% tab title="Output" %}
```
Body> We may need to re-think the init sequence...
✅ New comment added!
refs/heads/issues/1#50
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The**`-i`**flag is not required if you are already checked into the issue.
{% endhint %}

## Add a Reply

Similar to comments, a reply is a commit that references the hash of another commit in the same branch. You can add a comment by providing the target commit hash using `--reply` or `-r` flags.

{% tabs %}
{% tab title="Bash" %}
```bash
kit issue create -i=1 --reply="0f67159cea65546...c861289160f"
```
{% endtab %}

{% tab title="Output" %}
```
Body> Something about the way it works...
✅ New comment added!
refs/heads/issues/1#2
```
{% endtab %}
{% endtabs %}

## Add a Reaction

A reaction adds an emoji to a comment being replied to. MakeOS supports the [v13.0](http://www.unicode.org/emoji/charts/emoji-list.html) emoji list which offers a large collection of emojis to enable collaborators to express themselves however they wish.

 Add reactions to a reply by using the `--reactions` or `-e` flags.

{% tabs %}
{% tab title="Bash" %}
```bash
kit issue create -i=1 --reply="0f67159cea65546...c861289160f" -e="smiling_face,sparkle"
```
{% endtab %}

{% tab title="Output" %}
```
Body> I cannot wait to see how...
✅ New comment added!
refs/heads/issues/1#2
```
{% endtab %}
{% endtabs %}

## List All Issues

List all issues in the repository with `list` command: 

{% tabs %}
{% tab title="Bash" %}
```bash
kit issue list
```
{% endtab %}

{% tab title="Output" %}
```
issue daba0231b9cd6882c0305ee7dda4380b35399f88 issues/2
Title:  Fix the config loader
Author: John email@example.com
Date:   Wed Aug  5 22:41:05 2020 +0100

    The thing has refused to load quickly...

issue 95a0d4a6de1af728dbb47a385ff59ed162b16166 issues/1
Title:  Noticing false warnings
Author: Snow example@example.com
Date:   Sun Aug  2 16:25:46 2020 +0100
ReplyTo:    ab91ed58a04a5ee3d81c06bd481700f7b27c75ec
Reactions:  ☺: 1, ❇️: 1

    Is it normal for the alert to fire on...
```
{% endtab %}
{% endtabs %}

The command above will list all issues ordered by their commit date in descending order. Use the  `--reverse`flag to reverse the order. You can also limit the number of issues returned with `--limit` or `-n` flags. 

## Read an Issue

Use the `read` command to read the comments of a specific issue. Supposing there is an issue with ID = `2`, it can be read like this:

{% tabs %}
{% tab title="Bash" %}
```bash
kit issue read 2
```
{% endtab %}

{% tab title="Output" %}
```
comments daba0231b9cd6882c0305ee7dda4380b35399f88 #0
Author:     John <email@example.com>
Title:      Fix the config loader
Date:       Wed Aug  5 22:41:05 2020 +0100
    
    The component has refused to load quickly...
```
{% endtab %}
{% endtabs %}

Like the list command, it will list all comments ordered by their commit date in descending order. Use `--reverse` to reverse the order. You can also limit the number of comments returned with `--limit` or `-n` flags.

## Close an Issue

Close an issue with the `close`command. Supposing we want to close an issue with ID = `2`, we can do it with the command below:

```bash
kit issue close 2
```

Once an issue has been closed and pushed to remote, new comments will not be accepted unless the comment include a directive to re-opened the issue.

## Re-open an Issue

To reopen a closed issue, use the `reopen` command. The command below will reopen an issue with an ID of `2`.

```bash
kit issue reopen 2
```

It creates a new comment that includes a directive in the front-matter section instructing the network to update the issue's state to “open”.

## Check Issue Status

If you want to know the status of an issue, you can use `status` command.

```text
kit issue status 2
```

The command prints either `opened` or `closed`.

