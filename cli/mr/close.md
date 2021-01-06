---
id: close
title: Close Issue
sidebar_label: close
---

# close

The `close` command allows a user to close a merge request. The signer must have the `update` permission to push an update that closes an existing merge request.

## Usage

```bash
kit mr close [options] [<mergeReqId>]
```

```text
Usage:
  kit mr close [flags] [<mergeReqId>]

Flags:
  -f, --force   Forcefully create the close comment (uncommitted changes will be lost)
  -h, --help    help for close
```

## Arguments

`mergeReqId` - The numeric ID or reference name of the merge request. e.g. `1` or `refs/heads/merges/1` or `merges/1`.

## Options

* `-f, --force` - Forcefully add a new comment that flags the merge request as closed.  
* `-h, --help` - Prints out a help message.

## Example

```bash
kit mr close "1"
```

