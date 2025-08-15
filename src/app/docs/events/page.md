---
title: Events
nextjs:
  metadata:
    title: Events
    description: Run shell commands on Walker lifecycle hooks like on_launch, on_selection, on_exit, and query changes.
---

Walker can execute shell commands on lifecycle events. Configure under `[events]` in your config.

## Hooks

- on_launch: when the UI opens
- on_activate: when the window receives focus
- on_selection: when an entry is activated
- on_exit: when the UI closes
- on_query_change: whenever the query string changes

## Example

```toml
[events]
on_launch = "notify-send 'Walker' 'Opened'"
on_selection = "paplay /usr/share/sounds/freedesktop/stereo/message.oga"
on_exit = "notify-send 'Walker' 'Closed'"
```

Notes:

- Commands run in a shell; keep them idempotent and quick.
- Use environment variables if needed; see `.env` support via `~/.config/walker/.env`.

