---
title: Emojis
nextjs:
  metadata:
    title: Emojis
    description: Search emoji and copy them to the clipboard, with history and typeahead.
---

Search emojis and copy them to the clipboard.

## Configure

```toml
[builtins.emojis]
name = "emojis"
icon = "face-smile"
placeholder = "Emojis"
switcher_only = true
history = true
typeahead = true
exec = "wl-copy"
show_unqualified = false
```

Enter copies the emoji; history keeps recent choices handy.
