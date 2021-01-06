---
id: list
title: List Merge Requests
sidebar_label: list
---

# list

The `list` command lets you list all merge requests in a repository. The returned list is ordered by the most recent merge request.

## Usage

```bash
kit mr list [options]
```

```text
Usage:
  kit mr list [flags]

Flags:
  -d, --date string     Set date format (default "Mon Jan _2 15:04:05 2006 -0700")
  -f, --format string   Set output format
  -h, --help            help for list
  -n, --limit int       Limit the number of records to returned
      --reverse         Return the result in reversed order
```

## Options

* `-n, --limit` - Limit the number of merge requests to return.
* `--reverse` - Reverses the order from descending \(latest\) to ascending \(oldest\).  
* `-d, --date` - Provide a different date format. 
* `-f, --format` - Format the output for each merge request. These are the supported verbs:
  * `%i`: Index of the post
  * `%bb`: Base branch name
  * `%bh`: Base branch hash
  * `%tb`: Target branch name
  * `%th`: Target branch hash
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

```bash
kit mr list
```

