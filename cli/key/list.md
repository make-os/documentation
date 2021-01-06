---
id: list
title: List Keys
sidebar_label: list
---

# list

The `list` command will print out all keys in the keystore. Keys marked as _push_ keys are also listed and identified by their push key address.

## Usage

```text
kit key list [options]
```

```text
Usage:
  kit key list [flags]

Flags:
  -h, --help   help for list
```

## Options

* `-h, --help` - Prints out a help message.

## Example

{% tabs %}
{% tab title="Bash" %}
```bash
kit key list
```
{% endtab %}

{% tab title="Output" %}
```bash
    Address                                     Date         Created Tag(s) 
[0] os1qfrysysaawvjlgfz5ecqv569adkkw7sxudy36u   2 weeks ago 
[1] pk1wfx7vp8qfyv98cctvamqwec5xjrj48tpkfwme7   2 weeks ago  (unprotected)
```
{% endtab %}
{% endtabs %}



