---
id: fetch
title: Fetch a Merge Request
sidebar_label: fetch
---

# fetch

The `fetch` command is used to fetch the base or target branch of a merge request. 

## Usage

```bash
kit mr fetch [options] [[remote] id]
```

```text
Usage:
  kit mr fetch [flags] [[remote] id]

Flags:
  -b, --base          Fetch the base branch instead of the target branch
      --force-fetch   Forcefully fetch the branch (uncommitted changes will be lost)
  -h, --help          help for fetch
```

## Arguments

* `remote` - \(Optional\) The name of the remote to fetch from \(Default: origin\).
* `id` - The merge request ID. 

## Options

* `-b, --base` - Instead of checking out the target branch by default, check out the base branch.
* `--force-fetch` - Allows the merge request branch to be forcefully fetched.
* `-h, --help` - Prints out a help message.

## Example

```bash
kit mr fetch "1"
```

