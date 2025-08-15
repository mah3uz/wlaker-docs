---
title: Applications
nextjs:
  metadata:
    title: Applications
    description: Search and launch desktop applications with actions, history, and context-aware options.
---

Search and launch desktop applications.

## Configure

```toml
[builtins.applications]
name = "applications"
placeholder = "Applications"
prioritize_new = true
hide_actions_with_empty_query = true
context_aware = true
refresh = true
show_sub_when_single = true
show_icon_when_single = true
show_generic = true
history = true
icon = "applications-other"

[builtins.applications.actions]
enabled = true
hide_category = false
hide_without_query = true
```

Tips:

- Enable `actions` to show app actions (open website, etc.).
- `context_aware` can surface context-specific apps.
