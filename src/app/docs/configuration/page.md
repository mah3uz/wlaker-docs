---
title: Configuration
nextjs:
  metadata:
    title: Configuration
    description: Complete configuration guide for Walker including all available options.
---

Walker is configured through `~/.config/walker/config.toml`. This guide covers all available configuration options.

## Configuration File Location

- Default: `~/.config/walker/config.toml`
- Created automatically on first run
- Reference: `resources/config.toml` in the Walker repository

## General Settings

### Window Behavior

```toml
force_keyboard_focus = false    # Force keyboard focus to stay in Walker
close_when_open = true          # Close if invoked while already open
click_to_close = true           # Close when clicking outside content area
selection_wrap = false          # Wrap list navigation at top/bottom
disable_mouse = false           # Disable mouse on input and list
debug = false                   # Enable debug output
```

### Search Settings

```toml
global_argument_delimiter = "#"     # Delimiter for passing arguments
                                    # Example: firefox#https://example.com
                                    # Part after # is passed as argument

exact_search_prefix = "'"           # Prefix to disable fuzzy search
                                    # Example: 'firefox will match exactly
```

### Theme

```toml
theme = "default"              # Theme name to use
                               # Must exist in ~/.config/walker/themes/
```

## Shell Integration

Configure layer-shell anchoring (Wayland):

```toml
[shell]
anchor_top = true
anchor_bottom = true
anchor_left = true
anchor_right = true
```

## Placeholders

Customize placeholder text for input field and empty results:

```toml
[placeholders]
# Default placeholder for all providers
"default" = { input = "Search", list = "No Results" }

# Provider-specific placeholders
"desktopapplications" = { input = "Launch App", list = "No Applications" }
"files" = { input = "Browse Files", list = "No Files Found" }
"calc" = { input = "Calculate", list = "Enter Expression" }
"runner" = { input = "Run Command", list = "No Commands" }
"websearch" = { input = "Search Web", list = "" }
"clipboard" = { input = "Clipboard", list = "Clipboard Empty" }
"symbols" = { input = "Symbol", list = "No Symbols" }
"todo" = { input = "Todo", list = "No Todos" }

# For custom menus
"menus:mymenu" = { input = "My Menu", list = "No Items" }
```

## Keybindings

Define global keybindings. See [Keybindings](keybindings.md) for details.

```toml
[keybinds]
close = ["Escape"]
next = ["Down"]
previous = ["Up"]
toggle_exact = ["ctrl e"]           # Toggle exact search mode
resume_last_query = ["ctrl r"]      # Resume last query (service mode)
quick_activate = ["F1", "F2", "F3", "F4"]  # Quick activation keys
```

Valid modifier keys: `ctrl`, `alt`, `shift`, `super`

For key values, see [GDK key values](https://github.com/gtk-rs/gtk4-rs/blob/0.9/gdk4/sys/src/lib.rs#L302).

Example: `ctrl semicolon` maps to `GDK_KEY_semicolon`.

## Providers Configuration

### Default Providers

```toml
[providers]
# Providers queried by default (when no prefix used)
default = [
  "desktopapplications",
  "calc",
  "runner",
  "menus",
  "websearch",
]

# Providers shown when search is empty
empty = ["desktopapplications"]

# Global max results (can be overridden per provider)
max_results = 50
```

### Provider Sets

Create custom sets of providers that can be launched together:

```toml
[providers.sets]

# Example: custom launcher set
[providers.sets.mylauncher]
default = ["desktopapplications", "runner", "calc"]
empty = ["desktopapplications"]

# Example: file management set
[providers.sets.files]
default = ["files", "runner"]
empty = ["files"]

# Launch with: walker -s mylauncher
```

### Max Results Per Provider

```toml
[providers.max_results_provider]
desktopapplications = 20
files = 30
runner = 50
websearch = 10
```

### Provider Prefixes

Define prefixes to quickly access specific providers:

```toml
[[providers.prefixes]]
prefix = ";"
provider = "providerlist"       # Provider switcher

[[providers.prefixes]]
prefix = ">"
provider = "runner"             # Command runner

[[providers.prefixes]]
prefix = "/"
provider = "files"              # File browser

[[providers.prefixes]]
prefix = "."
provider = "symbols"            # Symbol picker

[[providers.prefixes]]
prefix = "!"
provider = "todo"               # Todo list

[[providers.prefixes]]
prefix = "="
provider = "calc"               # Calculator

[[providers.prefixes]]
prefix = "@"
provider = "websearch"          # Web search

[[providers.prefixes]]
prefix = ":"
provider = "clipboard"          # Clipboard history

# Custom menu prefix
[[providers.prefixes]]
prefix = "+"
provider = "menus:mymenu"       # Your custom menu
```

## Provider-Specific Configuration

### Clipboard

```toml
[providers.clipboard]
time_format = "%d.%m. - %H:%M"  # strftime format for timestamps
```

## Provider Actions

Define actions available for each provider. Actions determine what happens when you interact with items.

```toml
[providers.actions]

# Fallback actions for providers without specific actions
fallback = [
  { action = "menus:open", label = "open", after = "Nothing" },
  { action = "erase_history", label = "clear hist", bind = "ctrl h", after = "AsyncReload" },
]

# Dmenu mode actions
dmenu = [
  { action = "select", default = true, bind = "Return" }
]

# Provider list
providerlist = [
  { action = "activate", default = true, bind = "Return", after = "ClearReload" },
]

# Bluetooth
bluetooth = [
  { action = "find", global = true, bind = "ctrl f", after = "AsyncClearReload" },
  { action = "trust", bind = "ctrl t", after = "AsyncReload" },
  { action = "untrust", bind = "ctrl u", after = "AsyncReload" },
  { action = "pair", bind = "Return", after = "AsyncReload" },
  { action = "remove", bind = "ctrl d", after = "AsyncReload" },
  { action = "connect", bind = "Return", after = "AsyncReload" },
  { action = "disconnect", bind = "Return", after = "AsyncReload" },
]

# Arch Linux packages
archlinuxpkgs = [
  { action = "install", bind = "Return", default = true },
  { action = "remove", bind = "Return" },
]

# Calculator
calc = [
  { action = "copy", default = true, bind = "Return" },
  { action = "delete", bind = "ctrl d", after = "AsyncReload" },
  { action = "save", bind = "ctrl s", after = "AsyncClearReload" },
]

# Web search
websearch = [
  { action = "search", default = true, bind = "Return" }
]

# Desktop applications
desktopapplications = [
  { action = "start", default = true, bind = "Return" },
  { action = "start:keep", label = "open+next", bind = "shift Return", after = "KeepOpen" },
  { action = "pin", bind = "ctrl p", after = "AsyncReload" },
  { action = "unpin", bind = "ctrl p", after = "AsyncReload" },
  { action = "pinup", bind = "ctrl n", after = "AsyncReload" },
  { action = "pindown", bind = "ctrl m", after = "AsyncReload" },
]

# File browser
files = [
  { action = "open", default = true, bind = "Return" },
  { action = "opendir", label = "open dir", bind = "ctrl Return" },
  { action = "copypath", label = "copy path", bind = "ctrl shift c" },
  { action = "copyfile", label = "copy file", bind = "ctrl c" },
]

# Todo list
todo = [
  { action = "save", default = true, bind = "Return", after = "ClearReload" },
  { action = "delete", bind = "ctrl d", after = "ClearReload" },
  { action = "active", bind = "Return", after = "ClearReload" },
  { action = "inactive", bind = "Return", after = "ClearReload" },
  { action = "done", bind = "ctrl f", after = "ClearReload" },
  { action = "clear", bind = "ctrl x", after = "ClearReload", global = true },
]

# Command runner
runner = [
  { action = "run", default = true, bind = "Return" },
  { action = "runterminal", label = "run in terminal", bind = "shift Return" },
]

# Symbols
symbols = [
  { action = "run_cmd", label = "select", default = true, bind = "Return" },
]

# Unicode
unicode = [
  { action = "run_cmd", label = "select", default = true, bind = "Return" },
]

# Clipboard
clipboard = [
  { action = "copy", default = true, bind = "Return" },
  { action = "remove", bind = "ctrl d", after = "ClearReload" },
  { action = "remove_all", global = true, label = "clear", bind = "ctrl shift d", after = "ClearReload" },
  { action = "toggle_images", global = true, label = "toggle images", bind = "ctrl i", after = "ClearReload" },
  { action = "edit", bind = "ctrl o" },
]
```

### Action Properties

- `action` - The action name (provider-specific)
- `label` - Display label for the action (optional)
- `bind` - Keybinding to trigger the action
- `default` - Default action when pressing Enter (optional)
- `global` - Action available regardless of selection (optional)
- `after` - What happens after action execution:
  - `Nothing` - Walker stays open, no reload
  - `Close` - Walker closes
  - `KeepOpen` - Walker stays open
  - `Reload` - Reload results
  - `ClearReload` - Clear query and reload
  - `AsyncReload` - Reload asynchronously
  - `AsyncClearReload` - Clear and reload asynchronously

## Example Configurations

### Minimal Configuration

```toml
theme = "default"

[providers]
default = ["desktopapplications", "runner"]
empty = ["desktopapplications"]

[keybinds]
close = ["Escape"]
next = ["Down"]
previous = ["Up"]
```

### Power User Configuration

```toml
force_keyboard_focus = true
close_when_open = true
click_to_close = true
selection_wrap = true
exact_search_prefix = "'"
theme = "custom"
debug = false

[shell]
anchor_top = true
anchor_bottom = false
anchor_left = true
anchor_right = true

[placeholders]
"default" = { input = ">>", list = "∅" }
"desktopapplications" = { input = ">> Launch", list = "No apps" }
"files" = { input = ">> Browse", list = "No files" }

[keybinds]
close = ["Escape", "ctrl q"]
next = ["Down", "ctrl j"]
previous = ["Up", "ctrl k"]
toggle_exact = ["ctrl e"]
resume_last_query = ["ctrl r"]
quick_activate = ["F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8"]

[providers]
default = [
  "desktopapplications",
  "calc",
  "runner",
  "files",
  "websearch",
  "clipboard",
]
empty = ["desktopapplications", "clipboard"]
max_results = 100

[providers.max_results_provider]
desktopapplications = 30
files = 50
runner = 50

[[providers.prefixes]]
prefix = ";"
provider = "providerlist"

[[providers.prefixes]]
prefix = ">"
provider = "runner"

[[providers.prefixes]]
prefix = "/"
provider = "files"

[[providers.prefixes]]
prefix = "="
provider = "calc"

[[providers.prefixes]]
prefix = ":"
provider = "clipboard"
```

## Validation

After editing the configuration, test it:

```bash
# Check for syntax errors
walker --debug

# Or just launch normally
walker
```

Walker will report any configuration errors on startup.

## Next Steps

- [Keybindings](/docs/keybindings) - Detailed keybinding reference
- [Provider Actions](/docs/provider-actions) - Complete action reference
- [Theming](/docs/theming) - Customize Walker's appearance
- [Providers](/docs/providers) - Learn about all providers
