---
title: Keybindings
nextjs:
  metadata:
    title: Keybindings
    description: Keyboard shortcuts and customization options for Walker.
---

Walker provides extensive keyboard control and customization options.

## Default Keybindings

### Global Navigation

| Key            | Action                    |
|----------------|---------------------------|
| `Escape`       | Close Walker              |
| `Down`/`↓`     | Next result               |
| `Up`/`↑`       | Previous result           |
| `Tab`          | Next result (alternative) |
| `Shift+Tab`    | Previous result           |

### Execution

| Key           | Action                           |
|---------------|----------------------------------|
| `Enter`       | Execute default action           |
| `Shift+Enter` | Execute without closing Walker   |

### Search Control

| Key      | Action                          |
|----------|---------------------------------|
| `Ctrl+E` | Toggle exact search mode        |
| `Ctrl+R` | Resume last query (service mode)|

### Quick Activation

| Key  | Action                  |
|------|-------------------------|
| `F1` | Activate 1st result     |
| `F2` | Activate 2nd result     |
| `F3` | Activate 3rd result     |
| `F4` | Activate 4th result     |

## Provider-Specific Keybindings

### Desktop Applications

| Key             | Action                        |
|-----------------|-------------------------------|
| `Enter`         | Launch application            |
| `Shift+Enter`   | Launch and keep Walker open   |
| `Ctrl+P`        | Pin/unpin application         |
| `Ctrl+N`        | Move pinned item up           |
| `Ctrl+M`        | Move pinned item down         |

### Files

| Key             | Action              |
|-----------------|---------------------|
| `Enter`         | Open file           |
| `Ctrl+Enter`    | Open parent directory|
| `Ctrl+Shift+C`  | Copy file path      |
| `Ctrl+C`        | Copy file           |

### Calculator

| Key      | Action              |
|----------|---------------------|
| `Enter`  | Copy result         |
| `Ctrl+D` | Delete from history |
| `Ctrl+S` | Save calculation    |

### Runner (Commands)

| Key           | Action                     |
|---------------|----------------------------|
| `Enter`       | Run command                |
| `Shift+Enter` | Run in terminal            |

### Clipboard

| Key             | Action                  |
|-----------------|-------------------------|
| `Enter`         | Copy to clipboard       |
| `Ctrl+D`        | Remove entry            |
| `Ctrl+Shift+D`  | Clear entire history    |
| `Ctrl+I`        | Toggle image display    |
| `Ctrl+O`        | Edit clipboard entry    |

### Todo

| Key      | Action                |
|----------|-----------------------|
| `Enter`  | Save todo / Toggle state |
| `Ctrl+D` | Delete todo           |
| `Ctrl+F` | Mark as done          |
| `Ctrl+X` | Clear completed todos |

### Bluetooth

| Key      | Action               |
|----------|----------------------|
| `Enter`  | Connect/disconnect   |
| `Ctrl+F` | Start device scan    |
| `Ctrl+T` | Trust device         |
| `Ctrl+U` | Untrust device       |
| `Ctrl+D` | Remove device        |

### Arch Linux Packages

| Key      | Action              |
|----------|---------------------|
| `Enter`  | Install/remove pkg  |

### Symbols & Unicode

| Key     | Action         |
|---------|----------------|
| `Enter` | Insert symbol  |

### Web Search

| Key     | Action         |
|---------|----------------|
| `Enter` | Open in browser|

### Provider List

| Key     | Action                 |
|---------|------------------------|
| `Enter` | Switch to provider     |

## Customizing Keybindings

Edit `~/.config/walker/config.toml` to customize keybindings.

### Global Keybindings

```toml
[keybinds]
close = ["Escape", "ctrl q"]              # Multiple bindings allowed
next = ["Down", "ctrl j"]
previous = ["Up", "ctrl k"]
toggle_exact = ["ctrl e"]
resume_last_query = ["ctrl r"]
quick_activate = ["F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8"]
```

### Provider Action Keybindings

```toml
[providers.actions]

# Example: Custom calculator bindings
calc = [
  { action = "copy", default = true, bind = "Return" },
  { action = "copy", bind = "ctrl c" },           # Additional binding
  { action = "delete", bind = "ctrl d", after = "AsyncReload" },
  { action = "save", bind = "ctrl s", after = "ClearReload" },
]

# Example: Custom application launcher bindings
desktopapplications = [
  { action = "start", default = true, bind = "Return" },
  { action = "start", bind = "ctrl o" },          # Alternative
  { action = "start:keep", bind = "shift Return", after = "KeepOpen" },
  { action = "pin", bind = "ctrl p", after = "AsyncReload" },
]
```

## Keybinding Format

### Valid Modifiers

- `ctrl` - Control key
- `alt` - Alt key
- `shift` - Shift key
- `super` - Super/Windows/Command key

### Combining Modifiers

```toml
# Single modifier
bind = "ctrl a"

# Multiple modifiers
bind = "ctrl shift a"
bind = "ctrl alt shift f"

# No modifier (just a key)
bind = "Return"
bind = "F1"
```

### Key Names

Walker uses GDK key names. Common keys:

**Special Keys:**
- `Return` (Enter)
- `Escape`
- `BackSpace`
- `Delete`
- `Tab`
- `space`

**Navigation:**
- `Up`, `Down`, `Left`, `Right`
- `Home`, `End`
- `Page_Up`, `Page_Down`

**Function Keys:**
- `F1` through `F12`

**Letters and Numbers:**
- `a` through `z`
- `0` through `9`

**Symbols:**
- `semicolon` (`;`)
- `colon` (`:`)
- `slash` (`/`)
- `backslash` (`\`)
- `period` (`.`)
- `comma` (`,`)
- `minus` (`-`)
- `plus` (`+`)
- `equal` (`=`)
- `bracketleft` (`[`)
- `bracketright` (`]`)
- `braceleft` (`{`)
- `braceright` (`}`)

For a complete list, see [GDK key values](https://github.com/gtk-rs/gtk4-rs/blob/0.9/gdk4/sys/src/lib.rs#L302).

The constant name `GDK_KEY_semicolon` means the key name is `semicolon`.

## Action Properties

When defining action keybindings:

```toml
{ action = "name", bind = "key combo", default = true, global = true, label = "Label", after = "Behavior" }
```

- `action` - Action identifier (required)
- `bind` - Keybinding (optional, if not default)
- `default` - Use this action for Enter key (optional)
- `global` - Available regardless of selection (optional)
- `label` - Display label (optional)
- `after` - Post-action behavior (optional)
  - `Nothing` - Stay open, no reload
  - `Close` - Close Walker
  - `KeepOpen` - Keep Walker open
  - `Reload` - Reload results
  - `ClearReload` - Clear and reload
  - `AsyncReload` - Async reload
  - `AsyncClearReload` - Async clear and reload

## Examples

### Vim-like Navigation

```toml
[keybinds]
close = ["Escape", "ctrl c"]
next = ["Down", "ctrl j"]
previous = ["Up", "ctrl k"]
```

### Extended Quick Activation

```toml
[keybinds]
quick_activate = [
  "F1", "F2", "F3", "F4", "F5", "F6", "F7", "F8",
  "ctrl 1", "ctrl 2", "ctrl 3", "ctrl 4"
]
```

### Custom Application Actions

```toml
[providers.actions]
desktopapplications = [
  { action = "start", default = true, bind = "Return" },
  { action = "start:keep", bind = "ctrl Return", after = "KeepOpen" },
  { action = "start:keep", bind = "shift Return", after = "KeepOpen" },
  { action = "pin", bind = "ctrl p", after = "AsyncReload" },
  { action = "unpin", bind = "ctrl shift p", after = "AsyncReload" },
  { action = "pinup", bind = "alt Up", after = "AsyncReload" },
  { action = "pindown", bind = "alt Down", after = "AsyncReload" },
]
```

### Custom File Manager Actions

```toml
[providers.actions]
files = [
  { action = "open", default = true, bind = "Return" },
  { action = "open", bind = "ctrl o" },
  { action = "opendir", label = "open parent", bind = "ctrl shift o" },
  { action = "opendir", bind = "alt Up" },
  { action = "copypath", label = "copy path", bind = "ctrl c" },
  { action = "copyfile", label = "copy file", bind = "ctrl shift c" },
]
```

## Debugging Keybindings

Enable debug mode to see keybinding information:

```toml
debug = true
```

Or run Walker with debug flag:

```bash
walker --debug
```

This will print keybinding events to help troubleshoot issues.

## Keybinding Conflicts

If multiple actions have the same keybinding:
1. Provider-specific bindings take precedence
2. The first defined binding wins
3. Global bindings are always available

To avoid conflicts:
- Use unique combinations for different actions
- Use modifiers to distinguish similar actions
- Check default bindings before adding custom ones

## Tips

1. **Multiple Bindings:** You can assign multiple keybindings to the same action:
   ```toml
   close = ["Escape", "ctrl q", "ctrl w"]
   ```

2. **Consistency:** Keep similar actions across providers using similar keys:
   ```toml
   # Use Ctrl+D for delete everywhere
   calc: { action = "delete", bind = "ctrl d" }
   clipboard: { action = "remove", bind = "ctrl d" }
   todo: { action = "delete", bind = "ctrl d" }
   ```

3. **Global Actions:** Mark frequently used actions as global:
   ```toml
   { action = "clear_all", bind = "ctrl shift d", global = true }
   ```

4. **Testing:** After changing keybindings, test immediately to ensure they work as expected.

## Next Steps

- [Provider Actions](/docs/provider-actions) - Complete action reference
- [Configuration](/docs/configuration) - General configuration
- [Providers](/docs/providers) - Learn about providers
