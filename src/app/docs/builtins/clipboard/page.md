---
title: Clipboard
nextjs:
  metadata:
    title: Clipboard
    description: Browse and reuse clipboard history with copy-on-enter and formatting options.
---

Browse clipboard history; copy items back with Enter.

## Configure

```toml
[builtins.clipboard]
name = "clipboard"
icon = "user-bookmarks"
placeholder = "Clipboard"
switcher_only = true
always_put_new_on_top = true
avoid_line_breaks = true
image_height = 300
max_entries = 10
exec = "wl-copy"
```
{% callout title="Tip" %}
Press `Shift+Backspace` to remove the selected entry from history.
{% /callout %}
