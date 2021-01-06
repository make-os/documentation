---
id: reopen
title: Reopen an Issue
sidebar_label: reopen
---

# reopen

The `reopen` command allows a closed issue to be reopened. The signer must have `update` policy right to push a reopens request.

## Usage

```bash
kit issue reopen [options] [<issueId>]
```

```text
Usage:
  kit issue reopen [flags] [<issueId>]

Flags:
  -f, --force   Forcefully create the reopen comment (uncommitted changes will be lost)
  -h, --help    help for close
```

## Arguments

`issueId` - The numeric ID or reference name of the issue. e.g. `1` or `refs/heads/issue/1` or `issue/1`.

## Options

* `-f, --force` - Forcefully add a new comment that flags the issue as closed. The user requires  `update` policy action to push a reopened issue. 
* `-h, --help` - Prints out a help message.

## Example

```bash
kit issue reopen "1"
```

