---
id: status
title: Get Status of a Merge Request
sidebar_label: status
---

# status

The `status` command returns the status of a merge request.

## Usage

```bash
kit mr status [options] [<mergeReqId>]
```

```text
Usage:
  kit mr status [flags] [<mergeReqId>]

Flags:
  -h, --help    help for close
```

## Arguments

`mergeReqId` - The numeric ID or reference name of the merge request. e.g. `1` or `refs/heads/merges/1` or `merges/1`.

## Options

* `-h, --help` - Prints out a help message.

## Example

```bash
kit mr close "1"
```

