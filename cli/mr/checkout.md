---
id: checkout
title: Checkout a Merge Request
sidebar_label: checkout
---

# checkout

The `checkout` command fetches and checks out the target or base branch of a merge request.

## Usage

```bash
kit mr checkout [options] [[remote] id]
```

```text
Usage:
  kit mr checkout [flags] [[remote] id]

Flags:
  -b, --base             Checkout the base branch instead of the target branch
  -f, --force-checkout   Forcefully checkout while ignoring unsaved local changes
      --force-fetch      Forcefully fetch the branch (uncommitted changes will be lost)
  -h, --help             help for checkout
  -y, --yes              Automatically select 'Yes' for all confirm prompts
```

## Arguments

* `remote` - \(Optional\) The name of the remote to fetch from \(Default: origin\).
* `id` - The merge request ID. 

## Options

* `-b, --base` - Instead of checking out the target branch by default, check out the base branch.
* `-f, --force-checkout` - Checks out the merge request branch irrespective of unsaved changes on the current branch. Unsaved changes will be lost.
* `--force-fetch` - Allows the merge request branch to be forcefully fetched.
* `-y, --yes` - Respond with ‘Yes’ in situations where user confirmation is required. 
* `-h, --help` - Prints out a help message.

## Example

```bash
kit mr checkout "1"
```

