---
id: get
title: Get Key
sidebar_label: get
---

# get

The `get` command finds a key in the keystore, unlocks it and prints it out.

## Usage

```text
kit key get [options] 
```

```text
Usage:
  kit key get [flags] <address>

Flags:
  -h, --help       help for get
      --show-key   Show the private key
```

## Arguments

* `addressOrIndex` - The address of the key or its index on the keystore. 

## Options

* `--show-key` - If set, the private key of the key will be printed out. By default, the command will not print out the private key. 
* `-h, --help` - Prints out a help message.

## Example

* Get a key using its keystore index.

{% tabs %}
{% tab title="Bash" %}
```bash
kit key get 1 --show-key
```
{% endtab %}

{% tab title="Output" %}
```
Enter your passphrase to unlock the key
Passphrase> ******
✅ Key revealed successfully!
- User Address: os1wfx7vp8qfyv98cctvamqwec5xjrj48tpklxklh
- Push Address: pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7
- Public Key: 49G1iGk8fY7RQcJQ7LfQdThdyfaN8dKfxhGQSh8uuNaK35CgazZ
- Private Key: wetT9rgtetCHJV69oGCLpqQ8MiNTzB9...ipaEUyaKgi8QGmzRUPU1SmrfNSy4j7DDJ
```
{% endtab %}
{% endtabs %}

* Get a key using its address.

{% tabs %}
{% tab title="Bash" %}
```bash
kit key get os1wfx7vp8qfyv98cctvamqwec5xjrj48tpklxklh  --show-key
```
{% endtab %}

{% tab title="Output" %}
```
Enter your passphrase to unlock the key
Passphrase> ******
✅ Key revealed successfully!
- User Address: os1wfx7vp8qfyv98cctvamqwec5xjrj48tpklxklh
- Push Address: pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7
- Public Key: 49G1iGk8fY7RQcJQ7LfQdThdyfaN8dKfxhGQSh8uuNaK35CgazZ
- Private Key: wetT9rgtetCHJV69oGCLpqQ8MiNTzB9...ipaEUyaKgi8QGmzRUPU1SmrfNSy4j7DDJ
```
{% endtab %}
{% endtabs %}

* Get a key using its push key address.

{% tabs %}
{% tab title="Bash" %}
```bash
kit key get pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7  --show-key
```
{% endtab %}

{% tab title="Output" %}
```
Enter your passphrase to unlock the key
Passphrase> ******
✅ Key revealed successfully!
- User Address: os1wfx7vp8qfyv98cctvamqwec5xjrj48tpklxklh
- Push Address: pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7
- Public Key: 49G1iGk8fY7RQcJQ7LfQdThdyfaN8dKfxhGQSh8uuNaK35CgazZ
- Private Key: wetT9rgtetCHJV69oGCLpqQ8MiNTzB9...ipaEUyaKgi8QGmzRUPU1SmrfNSy4j7DDJ
```
{% endtab %}
{% endtabs %}

