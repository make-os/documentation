---
id: create
title: Create Merge Request
sidebar_label: create
---

# create

The `create` command lets you create a merge request or to add a comment to an existing merge request.

### Usage

```bash
kit mr create [options]
```

```text
Usage:
  kit mr create [flags]

Flags:
      --base string              Specify the base branch name
      --baseHash string          Specify the current hash of the base branch
  -b, --body string              The merge request message (max. 8 KB)
  -c, --close                    Close the merge request
      --editor string            Specify an editor to use instead of the git configured editor
  -f, --force                    Forcefully create the close comment (uncommitted changes will be lost)
  -h, --help                     help for create
  -i, --id int                   Specify a unique merge request number
      --new                      Force a new merge request to be created instead of adding a comment to HEAD
      --no-body                  Skip prompt for the merge request body
  -e, --reactions strings        Add reactions to a reply (max. 10)
  -o, --reopen                   Re-open a closed merge request
  -r, --reply string             Specify the hash of a comment to respond to
      --target string            Specify the target branch name
      --targetHash string        Specify the hash of the target branch
  -t, --title string             The merge request title (max. 250 B)
  -u, --use-editor core.editor   Use git's core.editor program to write the body
```

### Options

* `id` - Provide the ID of the merge request; Must be a number with not more than 16 characters in length. For example, if the ID is `10`, then the merge request reference will be `refs/heads/merges/10`. If a merge request exists with the matching ID, a comment will be added to the existing merge request. 
* `base` - The name of the branch where the updates from a different branch will be merged in.
* `baseHash` - The current commit hash of the base branch. If  `~`  is used, it will set it to the recent commit hash of the base branch. If `.` is used, it will set it to the recent hash of the current \(HEAD\) branch. 
* `target` - The name of the branch containing updates that will be merged into the base branch.
* `targetHash` - The current commit hash of the target branch. If  `~`  is used, it will set it to the recent commit hash of the target branch. If `.` is used, it will set it to the recent hash of the current \(HEAD\) branch. 
* `-t, --title` - The title of the merge request. Required only when creating a new merge request. If unset, a prompt will be started to ask for it.
* `-b, --body` - The body of the merge request or comment. If unset, a prompt will be started to ask for it.
* `-l, --labels` - Add up to 10 labels to the merge request. 
* `-a, --assignees` - Add up to 10 assignees to the merge request.
* `-e, --reactions` - Provide up to 10 reactions to a comment. Supports Unicode v13.0 emoji list. Note: emoji short names with spaces must replace them with underscore \(\_\) character. For example, `upside-down face` becomes `upside-down_face`. 
* `-r, --reply` - Specify the hash of a comment in an existing merge request you wish to respond to. If provided, reactions will be addressed to the target comment.
* `-c, --close` - Close a merge request. The user must have  `update`  rights to successfully push a closed merge request reference.
* `-o, --reopen` - Reopen a closed merge request. The user must have  `update`  rights to successfully push the reopened merge request reference.
* `--editor` - Specify an editor program to use to write the body instead of a prompt or  `-b` flag.
* `-u, --use-editor` - Similar to `--editor` but uses default git editor set in `core.editor`.
* `--new` - While checked into a merge request branch, force the command to create a new merge request instead of adding a comment to the checked out merge request.  Note: If the checked out branch is dirty, it will fail without using `--force` to ignore unsaved changes. 
* `--no-body` - Prevent the command from starting a prompt to ask the body. 
* `--force` - Ignore unsaved changes to the currently checked out branch. Unsaved updates will be lost.  

### Example

* Create a merge request

{% tabs %}
{% tab title="Bash" %}
```bash
kit mr create 
    --title="Made header visible" \
    --body="The header no longer hides behind..." \
    --base="master" \
    --baseHash="63fbec94fe9a8d5aef4a26f4598449888511e033" \
    --target="fix/header" \
    --targetHash="7c8330383196a9c52e41c06fd8b2f32fa4aaf98a" 
```
{% endtab %}

{% tab title="Output" %}
```
refs/heads/merges/1
```
{% endtab %}
{% endtabs %}

* Create a merge request that uses `~` to fetch the current base and target branch hashes.

{% tabs %}
{% tab title="Bash" %}
```bash
kit mr create 
    --title="Made header visible" \
    --body="The header no longer hides behind..." \
    --base="master" \
    --baseHash="~" \
    --target="fix/header" \
    --targetHash="~" 
```
{% endtab %}

{% tab title="Output" %}
```
refs/heads/merges/1
```
{% endtab %}
{% endtabs %}

