---
id: reopen
title: Reopen a Merge Request
sidebar_label: reopen
---

# reopen

The `reopen` command allows a closed merge request to be reopened. The signer must have `update` permission to push an update that reopens a merge request.

## Usage

```bash
kit mr reopen [options] [<mergeReqId>]
```

```text
Usage:
  kit mr reopen [flags] [<mergeReqId>]

Flags:
  -f, --force   Forcefully create the reopen comment (uncommitted changes will be lost)
  -h, --help    help for close
```

## Arguments

`mergeReqId` - The numeric ID or reference name of the merge request. e.g. `1` or `refs/heads/merges/1` or `merges/1`.

## Options

* `-f, --force` - Forcefully add a new comment that flags the merge request as closed.  
* `-h, --help` - Prints out a help message.

## Example

```bash
kit mr reopen "1"
```

