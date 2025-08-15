---
title: Runner
nextjs:
  metadata:
    title: Runner
    description: Search PATH and custom sources to run commands, with history, typeahead, and filters.
---

Search and run shell commands from PATH or custom sources.

## Configure

```toml
[builtins.runner]
name = "runner"
icon = "utilities-terminal"
placeholder = "Runner"
typeahead = true
history = true
refresh = true
generic_entry = false
use_fd = false
# includes = ["docker", "git"]
# excludes = ["shutdown"]
# shell_config = "~/.config/zsh/.zshrc"
```

Set `generic_entry = true` to show the raw query as a runnable entry.
