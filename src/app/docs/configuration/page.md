---
title: Configuration
nextjs:
  metadata:
    title: Configuration
    description: Global settings and module options — lists, search, activation mode, events, themes, and window behavior.
---

User configuration is merged with the built-in defaults and lives in:

- Linux: `~/.config/walker/config.toml`

On first run, Walker writes defaults and a theme into your user config.

## Top-level keys

```toml
terminal_title_flag = ""
locale = ""
close_when_open = false
monitor = ""
hotreload_theme = false
as_window = false
timeout = 0
force_keyboard_focus = false
js_runtime = "node"
# locations to search for themes and plugin scripts
theme_location = []
plugin_location = []
# theme name and optional base stack
theme = "default"
# theme_base = ["base1", "default"]

[keys]
# see Keys page for details

[events]
# see Events page

[list]
# see List options below

[search]
# see Search options below

[activation_mode]
# see Activation Mode below

[builtins]
# module-specific sections, see Built-ins pages
```

## List options

```toml
[list]
dynamic_sub = true
keyboard_scroll_style = "emacs"  # emacs|vim
max_entries = 50
show_initial_entries = true
single_click = true
visibility_threshold = 20
placeholder = "No Results"
```

## Search options

```toml
[search]
argument_delimiter = "#"
placeholder = "Search..."
delay = 0
resume_last_query = false
```

## Activation Mode

Shows activation labels for quick selection; labels can be letters or function keys.

```toml
[activation_mode]
labels = "jkl;asdf"
# disabled = false
# use_f_keys = false
```

## Events hooks

Run shell commands on lifecycle events.

```toml
[events]
on_activate = ""
on_selection = ""
on_exit = ""
on_launch = ""
on_query_change = ""
```

### Example: play a sound on selection

```toml
[events]
on_selection = "paplay /usr/share/sounds/freedesktop/stereo/message.oga"
```

## Window vs. Layer Shell

- Default uses Wayland Layer Shell. If unsupported, Walker falls back to a window.
- Force window mode:

```toml
as_window = true
```

## Theme files and CSS

- Layout/theme files live under `~/.config/walker/themes/` by default.
- Theme file name is the `theme` value with `.toml` (e.g., `default.toml`).
- CSS is loaded from `default.css` (prepended with pywal colors if available).
- Add extra search paths via `theme_location`.

See Themes & Layouts for structure and examples.

