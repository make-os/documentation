---
id: update
title: Update Key
sidebar_label: update
---

# update

The `update` command is used to update the passphrase of a key. You will be prompted to unlock the key using its existing passphrase before a new passphrase can be set.

## Usage

```bash
kit key update [options]
```

```text
Usage:
  kit key update [flags] <addressOrIndex>

Flags:
  -h, --help   help for update
```

## Arguments

* `addressOrIndex` - The address of the key or its index in the keystore.

## Options

* `-h, --help` - Prints out a help message.

## Example

```bash
kit key update os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u
```

