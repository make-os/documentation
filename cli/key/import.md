---
id: import
title: Import Key
sidebar_label: import
---

# import

The `import` command allows you to import a private key into the keystore. The private key is converted to a keystore key and locked using the provided passphrase.

## Usage

```text
kit key import [options] 
```

```text
Usage:
  kit key import [flags] <keyfile>

Flags:
  -h, --help   help for import
      --push   Mark as Push Key
```

## Arguments

* `keyfile` - The path to a file containing the private key or the raw private key.
* `--push` - Import the private key as a push key. 
* `-h, --help` - Prints out a help message.

## Example

```bash
kit key import "wetT9rgtetCHJV69oGCLpqQ8MiNTzB9d...aEUyaKgi8QGmzRUPU1SmrfNSy4j7DDJ"
```

