---
id: create
title: Create Issue
sidebar_label: create
---

# create

The `create` command lets you create an issue or to add a comment to an existing issue.

### Usage

```bash
kit issue create [options]
```

```text
Usage:
  kit issue create [flags]

Flags:
  -a, --assignees string    Specify push key of assignees to add to the issue/comment (max. 10)
  -b, --body string         The body of the issue (max. 8 KB)
  -c, --close               Close the issue
      --editor string       Specify an editor to use instead of the git configured editor
  -f, --force               Forcefully create comment (uncommitted changes will be lost)
  -h, --help                help for create
  -i, --id int              Specify a target issue number
  -l, --labels string       Specify labels to add to the issue/comment (max. 10)
      --new                 Force new issue to be created instead of adding a comment to HEAD
      --no-body             Skip prompt for issue body
  -e, --reactions strings   Add reactions to a reply (max. 10)
  -o, --reopen              Open a closed issue
  -r, --reply string        Specify the hash of a comment to respond to
  -t, --title string        The title of the issue (max. 250 B)
  -u, --use-editor          Use git's `core.editor` program to write the body
```

### Options

* `id` - Provide the ID of the issue; Must be a number with not more than 16 characters in length. For example, if the ID is `10`, then the issue reference will be `refs/heads/issues/10`. If an issue exists with the matching ID, a comment will be added to the existing issue. 
* `-t, --title` - The title of the issue. Required only when creating a new issue. If unset, a prompt will be started to ask for it.
* `-b, --body` - The body of the issue or comment. If unset, a prompt will be started to ask for it.
* `-l, --labels` - Add up to 10 labels to the issue. 
* `-a, --assignees` - Add up to 10 assignees to the issue.
* `-e, --reactions` - Provide up to 10 reactions to a comment. Supports Unicode v13.0 emoji list. Note: emoji short names with spaces must replace them with underscore \(\_\) character. For example, `upside-down face` becomes `upside-down_face`. 
* `-r, --reply` - Specify the hash of a comment in an existing issue you wish to respond to. If provided, reactions will be addressed to the target comment.
* `-c, --close` - Close an issue. The user must have  `update`  rights to successfully push a closed issue reference.
* `-o, --reopen` - Reopen a closed issue. The user must have  `update`  rights to successfully push the reopened issue reference.
* `--editor` - Specify an editor program to use to write the body instead of a prompt or  `-b` flag.
* `-u, --use-editor` - Similar to `--editor` but uses default git editor set in `core.editor`.
* `--new` - While checked into an issue branch, force the command to create a new issue instead of adding a comment to the checked-out issue.  Note: If the checked out branch is dirty, it will fail without using `--force` to ignore unsaved changes. 
* `--no-body` - Prevent the command from starting a prompt to ask for the body. 
* `--force` - Ignore unsaved changes to the currently checked out branch. Unsaved updates will be lost.  

### Example

* Create an issue using `--title` and `--body` flags.

{% tabs %}
{% tab title="Bash" %}
```bash
kit issue create \
    --title="header not visible" \
    --body="i am unable to see the header..."
```
{% endtab %}

{% tab title="Output" %}
```
refs/heads/issues/1
```
{% endtab %}
{% endtabs %}

* Create an issue with an explicitly provided issue ID.

```bash
kit issue create --id="123"
```

* Reply to a comment in an issue and add reactions.

```bash
kit issue create \
    --id="123" \
    --reply="63fbec94fe9a8d5aef4a26f4598449888511e033" \
    --reactions="smile,star-struck" \
    --title="header not visible" \
    --body="i am unable to see the header..." \
```



