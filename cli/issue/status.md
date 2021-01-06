---
id: status
title: Get Status of an Issue
sidebar_label: status
---

# status

The `status` command returns the status of an issue.

## Usage

```bash
kit issue status [options] [<issueId>]
```

```text
Usage:
  kit issue status [flags] [<issueId>]

Flags:
  -h, --help    help for close
```

## Arguments

`issueId` - The numeric ID or reference name of the issue. e.g. `1` or `refs/heads/issue/1` or `issue/1`.

## Options

* `-h, --help` - Prints out a help message.

## Example

{% tabs %}
{% tab title="Bash" %}
```bash
kit issue status "1"
```
{% endtab %}

{% tab title="Output" %}
```
"open"  # or 'closed'
```
{% endtab %}
{% endtabs %}

