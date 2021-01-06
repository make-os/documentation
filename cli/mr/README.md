# mr

The `mr` command allows you to create, view and manage merge requests.

To see a list of sub-commands, run `kit mr`

```text
Usage:
  kit mr [flags]
  kit mr [command]

Available Commands:
  checkout    Checkout a merge request target or base branch
  close       Close a merge request
  create      Create a merge request or add a comment to an existing one
  fetch       Fetch a merge request target or base branch
  list        List merge requests
  read        Read a merge request
  reopen      Reopen a closed merge request
  status      Get the status of a merge request

Flags:
      --no-pager   Prevent output from being piped into a pager
  -h, --help       help for mr
```

## Global Options

* `--no-pager` - Disable the use of a pager to render lengthy output. 
* `-h, --help` - Print out the commands help message.

