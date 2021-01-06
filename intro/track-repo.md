---
id: track-repo
title: Track a Repository
sidebar_label: Track a Repository
description: >-
  This section will teach you how to track and synchronize with specific
  repositories as opposed to tracking all repositories on the network.
---

# Track a Repository

By default, Kit will track and synchronize all repositories ever created on the network. 

Even when you do not know or like the repository, if you run a full node, that node will fetch all updates of all these repositories. 

While some users may choose to run their nodes in this mode to support the network, it may not be feasible for many users as the network becomes popular and widely utilized. 

Kit supports a tracking mode that allows you to specify any number of repositories you wish to track.

## Track a Repository

Kit provides `--repo.track` options on both the `start` and `console` commands. When starting Kit, specify a repo to track like this:

```bash
kit start --repo.track="my-repo"
```

You can pass as many `--repo.track` as you want. If you prefer, you may a pass comma-separated list like `--repo.track=repo1,repo2`.

### Using the Console

It is also possible to add repositories to track from the console using `repo.track` method.

```javascript
repo.track("my-repo,some-other-repo")
```

## Untrack a Repository

If you decide to untrack a repository that no longer interests you. You can use the `--repo.untrack` option on both the `start` and `console` commands.

```bash
kit start --repo.untrack="some-repo"
```

### Using the Console

The functionality is also available on the console:

```javascript
repo.untrack("some-repo")
```

## Untrack All Tracked Repository

If you want to go back to tracking and synchronizing all repositories on the network, you can use the`--repo.untrackall` option which like the other options is available on the `start` and `console` commands.

```bash
kit start --repo.untrackall
```

