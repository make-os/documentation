---
id: hook
title: Hooks Handler
sidebar_label: hook
---

# hook

The `hook` command provides handlers for responding to various git hooks or lifecycle events such as _pre-push_ event. 

This command may not be used directly since `kit config` will create and configure the hooks.

## Usage

```bash
kit repo hook [options] <remote>
```

```text
Handles git hook events

Usage:
  kit repo hook [flags] <remote>

Flags:
  -h, --help          help for hook
  -c, --post-commit   Executes the hook in post-commit mode
```

## Arguments

* `remote` - When the command is used as a _pre-push_ hook, the target remote of the push is passed via this argument.

## Options

* `-c, --post-commit` - Indicates that the hook was fired in response to git's `post-commit` hook event. 
* `-h, --help` - Prints out a help message.

