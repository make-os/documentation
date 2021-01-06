---
id: list
title: List Issue
sidebar_label: list
---

# list

The `list` command lets you list all issues in a repository beginning with the most recent.

## Usage

```bash
kit issue list [options]
```

```text
Usage:
  kit issue list [flags]

Flags:
  -d, --date string     Set date format (default "Mon Jan _2 15:04:05 2006 -0700")
  -f, --format string   Set output format
  -h, --help            help for list
  -n, --limit int       Limit the number of records to returned
      --reverse         Return the result in reversed order
```

## Options

* `-n, --limit` - Limit the number of issues to return.
* `--reverse` - Reverses the order from descending \(latest\) to ascending \(oldest\).  
* `-d, --date` - Provide a different date format. 
* `-f, --format` - Format the output for each issue. These are the supported verbs:
  * `%i`: Index of the post
  * `%a`: Author of the post
  * `%e`: Author email
  * `%t`: Title of the post
  * `%c`: The body/preview of the post
  * `%d`: Date of creation
  * `%H`: The full hash of the first comment
  * `%h`: The short hash of the first comment
  * `%n`: The reference name of the post
  * `%pk`: The push key address
* `-h, --help` - Prints out a help message.

## Example

```text
kit issue list
```

