---
id: close
title: Close Issue
sidebar_label: close
---

# close

The `close` command allows an issue to be closed. The signer must have `update` permission to push an update that closes an issue.

## Usage

```bash
kit issue close [options] [<issueId>]
```

```text
Usage:
  kit issue close [flags] [<issueId>]

Flags:
  -f, --force   Forcefully create the close comment (uncommitted changes will be lost)
  -h, --help    help for close
```

## Arguments

`issueId` - The numeric ID or reference name of the issue. e.g. `1` or `refs/heads/issue/1` or `issue/1`.

## Options

* `-f, --force` - Forcefully add a new comment that flags the issue as closed. 
* `-h, --help` - Prints out a help message.

## Example

```javascript
kit issue close "1"
```

