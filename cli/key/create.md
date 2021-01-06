---
id: create
title: Create Key
sidebar_label: create
---

# create

The `create` command is used to start a JavaScript console that connects to an already running local or remote Kit node.

### Usage

```text
kit key create [options]
```

```text
Usage:
  kit key create [flags]

Flags:
  -h, --help       help for create
      --nopass     Force key to be created with no passphrase
      --push       Mark as Push Key
  -s, --seed int   Provide a strong seed (not recommended)
```

### Options

* `--nopass` - Sets the encryption passphrase to the default, unsafe passphrase “passphrase” which essentially means the key is unprotected. This is not recommended. 
* `--push` - Mark the key as a _push_ key. This means the intent is to use the key for signing push requests. When the key is listed, the push key address will be printed out instead of a user address. 
* `-s, --seed` - Provide an integer to be used as the seed. This is not recommended and only used for testing situations where a key needs to be reproducible. 
* `-h, --help` - Prints out a help message.

### Example

* Create a regular key.

{% tabs %}
{% tab title="Bash" %}
```bash
kit key create
```
{% endtab %}

{% tab title="Output" %}
```
Your new key needs to be locked. Please enter a passphrase. 
Passphrase> ** 
Repeat Passphrase> ** 
✅ Key successfully created!
 - Address: os1dr67qxhhvkjmzhvn6s7jm3rh7a09wg3zewcjn0
```
{% endtab %}
{% endtabs %}

* Create a Push Key

{% tabs %}
{% tab title="Bash" %}
```bash
kit key create --push
```
{% endtab %}

{% tab title="Output" %}
```
Your new key needs to be locked. Please enter a passphrase. 
Passphrase> ** 
Repeat Passphrase> ** 
✅ Key successfully created!
 - Address: pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7
```
{% endtab %}
{% endtabs %}



