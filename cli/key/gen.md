---
id: gen
title: Generate Key
sidebar_label: gen
---

# gen

The `gen` command generates an ed25519 key pair.

## Usage

```bash
kit key gen [options]
```

```bash
Usage:
  kit key gen [flags]

Flags:
  -h, --help       help for gen
  -s, --seed int   Provide a strong seed (not recommended)
```

## Options

* `-s, --seed` - Provide an integer to be used as the seed. 
* `-h, --help` - Prints out a help message.

## Example

{% tabs %}
{% tab title="Bash" %}
```bash
kit key gen
```
{% endtab %}

{% tab title="Output" %}
```bash
Private Key: wZRxNmWoDvpvv5abPqXDHL...6ggmSLVrVqa7sWg6rqTCahvogmYugYpLGNDffAct
Public Key:  48YD57pjLkpx5pBaF87jvrHUg9adPkvpCM4nJxmw9W94wEUft6K
Account Address:  os132k9z96cryeq9dp4jva380rp6xeskdrdpup3l5
Push Address:  pk132k9z96cryeq9dp4jva380rp6xeskdrdp2fuea 
```
{% endtab %}
{% endtabs %}

