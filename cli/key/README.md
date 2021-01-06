# key

The `key` command provides the ability to create and manage keys encrypted and stored on the keystore.

To see a list of sub-commands, run `kit key`

```text
Usage:
  kit key command [flags]
  kit key [command]

Available Commands:
  create      Create a key.
  gen         Generate an ed25519 key
  get         Get a key
  import      Import an existing, unencrypted private key.
  list        List all accounts.
  update      Update a key

Flags:
  -h, --help          help for key
      --pass string   Password to unlock the target key and skip interactive mode
```

## Global Options

The command includes global options that can be set for all sub-commands.

* `--pass`  - Set the passphrase to unlock an existing key in cases where a key needs to be read.
* `-h, --help` - Print out a help message.

