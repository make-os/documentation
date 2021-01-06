---
id: read
title: Read a Merge Request
sidebar_label: read
---

# read

The `read` command lets you read all comments in a merge request.

## Usage

```bash
kit mr read [options] [<mergeReqId>]
```

```text
Usage:
  kit mr read [flags] [<mergeReqId>]

Flags:
  -d, --date string       Set date format (default "Mon Jan _2 15:04:05 2006 -0700")
  -f, --format string     Set output format
  -h, --help              help for read
  -n, --limit int         Limit the number of records returned
      --no-close-status   Hide the close status indicator
      --reverse           Return the result in reversed order
```

## Arguments

`mergeReqId` - The numeric ID or reference name of the merge request. e.g. `1` or `refs/heads/merges/1` or `merges/1`.

## Options

* `-n, --limit` - Limit the number of comments to return.
* `--reverse` - Reverses the order from descending \(latest\) to ascending \(oldest\).  
* `-d, --date` - Provide a different date format. 
* `-f, --format` - Format the output for each merge request. These are the supported verbs:
  * `%i`: Index of the comment
  * `%a`: Author of the comment
  * `%e`: Author email
  * `%t`: Title of the comment
  * `%c`: The body of the comment
  * `%d`: Date of creation
  * `%H`: The full hash of the comment
  * `%h`: The short hash of the comment
  * `%n`: The reference name of the post
  * `%l`: The label attached to the comment
  * `%as`: The assignees attached to the comment
  * `%r`: The short commit hash the current comment is replying to.
  * `%R`: The full commit hash the current comment is replying to.
  * `%rs`: The comment’s reactions.
  * `%pk`: The push key address
  * `%cl`: Flag for the close status of the post \(true/false\)
* `--no-close-status` - When a merge request is closed, it prevents the close indicator from being rendered.
* `-h, --help` - Prints out a help message.

## Example

```bash
kit mr read "1"
```

