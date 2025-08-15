---
title: Keys
nextjs:
  metadata:
    title: Keys
    description: Customize navigation, activation, and AI view keybindings including modifiers for alternate actions.
---

Customize navigation and activation keys in `[keys]`.

## Defaults

```toml
[keys]
accept_typeahead = ["tab"]
trigger_labels = "lalt"          # hold to show activation labels
next = ["down"]
prev = ["up"]
close = ["esc"]
remove_from_history = ["shift backspace"]
resume_query = ["ctrl r"]
toggle_exact_search = ["ctrl m"]

[keys.activation_modifiers]
keep_open = "shift"   # Shift+Enter keeps window open after activation
alternate = "alt"     # Alt+Enter triggers alt action

[keys.ai]
clear_session = ["ctrl x"]
copy_last_response = ["ctrl c"]
resume_session = ["ctrl r"]
run_last_response = ["ctrl e"]
```

Notes:

- Enter activates; Shift+Enter keeps window open; Alt+Enter triggers alt action.
- Exact match toggle wraps the query with a leading `'`.
- In AI view, AI-specific keybinds apply.

## Example: vim-like navigation

```toml
[keys]
next = ["down", "j"]
prev = ["up", "k"]
```
