---
title: Finder
nextjs:
  metadata:
    title: Finder
    description: Find files and directories, optionally using fd for performance with previews and actions.
---

Find files and directories. Can use `fd` for performance.

## Configure

```toml
[builtins.finder]
name = "finder"
icon = "folder"
placeholder = "Finder"
switcher_only = true
ignore_gitignore = true
refresh = true
concurrency = 8
preview_images = false
use_fd = false
fd_flags = "--ignore-vcs --type file --type directory"
cmd_alt = 'xdg-open "$(dirname "$HOME/%RESULT%")"'
```

Tip: Turn on `use_fd` if `fd` is installed for faster searches.
