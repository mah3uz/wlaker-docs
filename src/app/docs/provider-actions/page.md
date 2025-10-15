---
title: Provider Actions
nextjs:
  metadata:
    title: Provider Actions
    description: Learn about provider actions and how to customize them in Walker.
---

Actions define what happens when you interact with items from providers. This guide covers all available actions and how to customize them.

## Understanding Actions

Each provider has a set of actions that can be triggered via keybindings. Actions can:
- Execute immediately (e.g., launch an application)
- Modify data (e.g., pin an application, delete a clipboard entry)
- Change Walker's state (e.g., reload results, clear query)

### Action Properties

```toml
{ action = "action_name", bind = "key", default = true, global = true, label = "Display Label", after = "Behavior" }
```

**Properties:**
- `action` - Action identifier (required)
- `bind` - Keybinding to trigger the action
- `default` - This action runs on `Enter` (only one per provider)
- `global` - Action available regardless of item selection
- `label` - Display name for the action (optional)
- `after` - What happens after the action executes:
  - `Nothing` - Walker stays open, no changes
  - `Close` - Walker closes
  - `KeepOpen` - Walker stays open
  - `Reload` - Reload provider results
  - `ClearReload` - Clear query and reload
  - `AsyncReload` - Reload asynchronously
  - `AsyncClearReload` - Clear query and reload asynchronously

## Fallback Actions

Applied to providers without specific action definitions:

```toml
[providers.actions]
fallback = [
  { action = "menus:open", label = "open", after = "Nothing" },
  { action = "erase_history", label = "clear hist", bind = "ctrl h", after = "AsyncReload" },
]
```

## Provider-Specific Actions

### Desktop Applications

```toml
[providers.actions]
desktopapplications = [
  { action = "start", default = true, bind = "Return" },
  { action = "start:keep", label = "open+next", bind = "shift Return", after = "KeepOpen" },
  { action = "pin", bind = "ctrl p", after = "AsyncReload" },
  { action = "unpin", bind = "ctrl p", after = "AsyncReload" },
  { action = "pinup", bind = "ctrl n", after = "AsyncReload" },
  { action = "pindown", bind = "ctrl m", after = "AsyncReload" },
]
```

**Actions:**
- `start` - Launch the application
- `start:keep` - Launch and keep Walker open (for launching multiple apps)
- `pin` - Pin application to top of list
- `unpin` - Unpin application
- `pinup` - Move pinned application up
- `pindown` - Move pinned application down

**Use Cases:**
- Pin frequently used applications for quick access
- Launch multiple applications in sequence with `start:keep`
- Organize pinned applications with `pinup`/`pindown`

### Calculator

```toml
[providers.actions]
calc = [
  { action = "copy", default = true, bind = "Return" },
  { action = "delete", bind = "ctrl d", after = "AsyncReload" },
  { action = "save", bind = "ctrl s", after = "AsyncClearReload" },
]
```

**Actions:**
- `copy` - Copy result to clipboard
- `delete` - Remove calculation from history
- `save` - Save calculation for quick access

**Use Cases:**
- Save frequently used calculations (e.g., tax rates, conversions)
- Clean up calculation history

### Runner (Commands)

```toml
[providers.actions]
runner = [
  { action = "run", default = true, bind = "Return" },
  { action = "runterminal", label = "run in terminal", bind = "shift Return" },
]
```

**Actions:**
- `run` - Execute command silently
- `runterminal` - Execute command in terminal window

**Use Cases:**
- Run GUI applications with `run`
- Run CLI commands with `runterminal` to see output

### Files

```toml
[providers.actions]
files = [
  { action = "open", default = true, bind = "Return" },
  { action = "opendir", label = "open dir", bind = "ctrl Return" },
  { action = "copypath", label = "copy path", bind = "ctrl shift c" },
  { action = "copyfile", label = "copy file", bind = "ctrl c" },
]
```

**Actions:**
- `open` - Open file with default application
- `opendir` - Open parent directory in file manager
- `copypath` - Copy file path to clipboard
- `copyfile` - Copy file to clipboard

**Use Cases:**
- Quick file navigation and opening
- Copy file paths for terminal commands
- Drag & drop support (when applicable)

### Web Search

```toml
[providers.actions]
websearch = [
  { action = "search", default = true, bind = "Return" }
]
```

**Actions:**
- `search` - Open search in default browser

### Clipboard

```toml
[providers.actions]
clipboard = [
  { action = "copy", default = true, bind = "Return" },
  { action = "remove", bind = "ctrl d", after = "ClearReload" },
  { action = "remove_all", global = true, label = "clear", bind = "ctrl shift d", after = "ClearReload" },
  { action = "toggle_images", global = true, label = "toggle images", bind = "ctrl i", after = "ClearReload" },
  { action = "edit", bind = "ctrl o" },
]
```

**Actions:**
- `copy` - Copy selected entry to clipboard
- `remove` - Remove entry from history
- `remove_all` - Clear entire clipboard history (global)
- `toggle_images` - Show/hide image previews (global)
- `edit` - Edit clipboard entry text

**Use Cases:**
- Manage clipboard history
- Remove sensitive clipboard entries
- Toggle images for privacy or performance

### Todo

```toml
[providers.actions]
todo = [
  { action = "save", default = true, bind = "Return", after = "ClearReload" },
  { action = "delete", bind = "ctrl d", after = "ClearReload" },
  { action = "active", bind = "Return", after = "ClearReload" },
  { action = "inactive", bind = "Return", after = "ClearReload" },
  { action = "done", bind = "ctrl f", after = "ClearReload" },
  { action = "clear", bind = "ctrl x", after = "ClearReload", global = true },
]
```

**Actions:**
- `save` - Create new todo
- `delete` - Delete todo
- `active` - Mark todo as active
- `inactive` - Mark todo as inactive
- `done` - Mark todo as completed
- `clear` - Clear all completed todos (global)

**Use Cases:**
- Quick todo creation and management
- Track active tasks
- Clean up completed todos periodically

### Symbols & Unicode

```toml
[providers.actions]
symbols = [
  { action = "run_cmd", label = "select", default = true, bind = "Return" },
]

unicode = [
  { action = "run_cmd", label = "select", default = true, bind = "Return" },
]
```

**Actions:**
- `run_cmd` - Insert symbol/character (copies to clipboard or types)

### Provider List

```toml
[providers.actions]
providerlist = [
  { action = "activate", default = true, bind = "Return", after = "ClearReload" },
]
```

**Actions:**
- `activate` - Switch to selected provider

### Bluetooth

```toml
[providers.actions]
bluetooth = [
  { action = "find", global = true, bind = "ctrl f", after = "AsyncClearReload" },
  { action = "trust", bind = "ctrl t", after = "AsyncReload" },
  { action = "untrust", bind = "ctrl u", after = "AsyncReload" },
  { action = "pair", bind = "Return", after = "AsyncReload" },
  { action = "remove", bind = "ctrl d", after = "AsyncReload" },
  { action = "connect", bind = "Return", after = "AsyncReload" },
  { action = "disconnect", bind = "Return", after = "AsyncReload" },
]
```

**Actions:**
- `find` - Start device scanning (global)
- `trust` - Trust device
- `untrust` - Untrust device
- `pair` - Pair with device
- `remove` - Remove device from list
- `connect` - Connect to device
- `disconnect` - Disconnect from device

**Use Cases:**
- Complete Bluetooth management from Walker
- Quick device switching

### Arch Linux Packages

```toml
[providers.actions]
archlinuxpkgs = [
  { action = "install", bind = "Return", default = true },
  { action = "remove", bind = "Return" },
]
```

**Actions:**
- `install` - Install package (prompts for confirmation)
- `remove` - Remove package (prompts for confirmation)

**Use Cases:**
- Search and install packages without opening terminal
- Quick package removal

### Dmenu Mode

```toml
[providers.actions]
dmenu = [
  { action = "select", default = true, bind = "Return" }
]
```

**Actions:**
- `select` - Select item and output to stdout

**Use Cases:**
- Walker as a dmenu replacement
- Integration with scripts

## Customizing Actions

### Adding Custom Keybindings

Add alternative keybindings to existing actions:

```toml
[providers.actions]
desktopapplications = [
  { action = "start", default = true, bind = "Return" },
  { action = "start", bind = "ctrl o" },           # Alternative binding
  { action = "start:keep", bind = "shift Return", after = "KeepOpen" },
  { action = "start:keep", bind = "ctrl Return", after = "KeepOpen" },  # Alternative
  { action = "pin", bind = "ctrl p", after = "AsyncReload" },
]
```

### Changing Default Actions

Change which action runs on `Enter`:

```toml
[providers.actions]
calc = [
  { action = "save", default = true, bind = "Return", after = "ClearReload" },  # Changed default
  { action = "copy", bind = "ctrl c" },
  { action = "delete", bind = "ctrl d", after = "AsyncReload" },
]
```

### Removing Actions

To disable an action, simply don't include it in the configuration. Walker will use built-in defaults for any actions you don't define.

### Global Actions

Mark actions as global so they work without selecting an item:

```toml
[providers.actions]
clipboard = [
  { action = "copy", default = true, bind = "Return" },
  { action = "remove_all", global = true, bind = "ctrl shift d", after = "ClearReload" },
  { action = "toggle_images", global = true, bind = "ctrl i", after = "ClearReload" },
]
```

## Advanced Usage

### Chaining Actions

While you can't directly chain actions, you can use the `after` property strategically:

```toml
{ action = "pin", bind = "ctrl p", after = "AsyncReload" }  # Pins and reloads
```

### Context-Aware Actions

Some actions behave differently based on context. For example, in the `desktopapplications` provider:
- `pin` - Pins an unpinned app
- `unpin` - Unpins a pinned app

Both can share the same keybinding, and Walker determines which to use based on the item's current state.

### Custom Labels

Customize action labels for clarity:

```toml
[providers.actions]
files = [
  { action = "open", default = true, bind = "Return" },
  { action = "opendir", label = "📁 parent dir", bind = "ctrl Return" },
  { action = "copypath", label = "📋 path", bind = "ctrl shift c" },
  { action = "copyfile", label = "📄 file", bind = "ctrl c" },
]
```

## Action Behavior Reference

### After Execution Behaviors

| Behavior           | Description                                    | Use Case                          |
|--------------------|------------------------------------------------|-----------------------------------|
| `Nothing`          | Walker stays open, no reload                   | Informational actions             |
| `Close`            | Walker closes                                  | Final actions                     |
| `KeepOpen`         | Walker stays open explicitly                   | Sequential operations             |
| `Reload`           | Reload current provider results                | Data modification                 |
| `ClearReload`      | Clear query and reload                         | Start fresh after action          |
| `AsyncReload`      | Reload asynchronously (non-blocking)           | Slow operations                   |
| `AsyncClearReload` | Clear and reload asynchronously                | Slow operations, start fresh      |

### Default vs Custom Actions

Walker has built-in default actions for all providers. When you define custom actions in your config, you override the defaults completely. To preserve some defaults while customizing others, you must explicitly include them.

**Example:**

```toml
# This replaces ALL default actions for desktopapplications
[providers.actions]
desktopapplications = [
  { action = "start", default = true, bind = "Return" },
  # Must include other actions you want to keep
  { action = "pin", bind = "ctrl p", after = "AsyncReload" },
]
```

## Troubleshooting

### Action Not Working

1. **Check keybinding conflicts** - Ensure the keybinding isn't used by another action
2. **Verify action name** - Action names are provider-specific and case-sensitive
3. **Check `default` property** - Only one action per provider can have `default = true`
4. **Enable debug mode** - Set `debug = true` in config to see action execution

### Action Partially Works

Some actions require Elephant provider features. Ensure:
1. Provider is installed and up to date
2. Elephant is running and configured correctly
3. Provider has necessary permissions (e.g., Bluetooth needs system permissions)

### Global Actions Not Available

Global actions require:
1. `global = true` in action definition
2. Proper keybinding (must not conflict with global Walker keybindings)

## Examples

### Minimal Configuration

```toml
[providers.actions]
# Only override what you need
desktopapplications = [
  { action = "start", default = true, bind = "Return" },
]
```

### Power User Configuration

```toml
[providers.actions]
desktopapplications = [
  { action = "start", default = true, bind = "Return" },
  { action = "start", bind = "ctrl o" },
  { action = "start:keep", bind = "shift Return", after = "KeepOpen" },
  { action = "start:keep", bind = "ctrl shift o", after = "KeepOpen" },
  { action = "pin", bind = "ctrl p", after = "AsyncReload" },
  { action = "unpin", bind = "ctrl shift p", after = "AsyncReload" },
  { action = "pinup", bind = "alt Up", after = "AsyncReload" },
  { action = "pindown", bind = "alt Down", after = "AsyncReload" },
]

files = [
  { action = "open", default = true, bind = "Return" },
  { action = "open", bind = "ctrl o" },
  { action = "opendir", label = "parent", bind = "ctrl shift o" },
  { action = "opendir", bind = "alt Up" },
  { action = "copypath", label = "path", bind = "ctrl c" },
  { action = "copyfile", label = "file", bind = "ctrl shift c" },
]

clipboard = [
  { action = "copy", default = true, bind = "Return" },
  { action = "copy", bind = "ctrl c" },
  { action = "remove", bind = "Delete" },
  { action = "remove", bind = "ctrl d", after = "ClearReload" },
  { action = "remove_all", global = true, bind = "ctrl shift Delete", after = "ClearReload" },
  { action = "toggle_images", global = true, bind = "ctrl i", after = "ClearReload" },
  { action = "edit", bind = "ctrl e" },
  { action = "edit", bind = "F2" },
]
```

## Next Steps

- [Keybindings](/docs/keybindings) - Keybinding reference
- [Configuration](/docs/configuration) - General configuration
- [Providers](/docs/providers) - Learn about providers
