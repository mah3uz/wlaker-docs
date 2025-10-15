---
title: Getting Started
nextjs:
  metadata:
    title: Getting Started
    description: Get started with Walker and learn the basic usage after installation.
---

This guide will help you start using Walker after installation.

## Prerequisites

Before starting, ensure:
1. Walker is installed (see [Installation](/docs/installation))
2. Elephant service is running
3. At least some Elephant providers are installed

## First Launch

Simply run:

```bash
walker
```

On first launch, Walker will create:
- Configuration file: `~/.config/walker/config.toml`
- Theme directory: `~/.config/walker/themes/`

## Basic Usage

### Searching

1. **Type to search** - Start typing and Walker will search across active providers
2. **Navigate results** - Use `↑` and `↓` arrow keys or `Tab`
3. **Execute** - Press `Enter` to run the selected item
4. **Close** - Press `Escape` to close Walker

### Provider Prefixes

Walker uses prefixes to quickly access specific providers:

| Prefix | Provider          | Description                    |
|--------|-------------------|--------------------------------|
| `;`    | providerlist      | Switch between providers       |
| `>`    | runner            | Run shell commands             |
| `/`    | files             | Browse files                   |
| `.`    | symbols           | Insert special symbols         |
| `!`    | todo              | Manage todo items              |
| `=`    | calc              | Calculator                     |
| `@`    | websearch         | Search the web                 |
| `:`    | clipboard         | Clipboard history              |

**Example:**
```bash
=2+2              # Opens calculator with "2+2"
/home/user/docs   # Opens file browser in that directory
>ls -la           # Prepares to run the command
@rust tutorial    # Searches web for "rust tutorial"
```

## Default Providers

Without a prefix, Walker queries these providers by default:
- Desktop Applications
- Calculator (for expressions starting with numbers/operators)
- Runner (for commands)
- Menus
- Websearch

## Common Workflows

### Launching Applications

Simply type the application name:
```text
firefox
code
```

### Running Commands

Use the `>` prefix or just type the command:
```text
>htop
>systemctl status
```

### Quick Calculations

Use `=` prefix or just type an expression:
```text
=2 + 2
=(50 * 1.19) - 10
```

### Finding Files

Use `/` to browse from a directory:
```text
/home/user/Documents
/etc/nginx
```

### Switching Providers

Use `;` to see all available providers:
```text
;
```

Then select one to switch to it exclusively.

## Quick Activation

Walker supports quick activation labels for the top results. Hold `Ctrl` and press:
- `F1` - Activate first result
- `F2` - Activate second result
- `F3` - Activate third result
- `F4` - Activate fourth result

This can be customized in the configuration.

## Running as a Service (Recommended)

For instant startup, run Walker as a background service:

```bash
# Start Walker service
walker --gapplication-service &

# Now launching Walker is instant
walker
```

### Automatic Service Start

You can make Walker start automatically on login:

**For systemd:**

Create `~/.config/systemd/user/walker.service`:

```ini
[Unit]
Description=Walker Launcher Service
PartOf=graphical-session.target

[Service]
ExecStart=/usr/bin/walker --gapplication-service
Restart=on-failure

[Install]
WantedBy=default.target
```

Then enable it:

```bash
systemctl --user enable --now walker.service
```

**For Hyprland/Window Managers:**

Add to your config:

```bash
# Hyprland
exec-once=walker --gapplication-service

# i3/sway
exec walker --gapplication-service
```

## Socket Launch (Advanced)

For even faster launching (if Walker service is running):

```bash
nc -U /run/user/1000/walker/walker.sock
```

You can bind this to a hotkey in your window manager for instant access.

**Note:** Socket launch doesn't support command-line arguments.

## Essential Keybindings

| Keybinding     | Action                          |
|----------------|--------------------------------|
| `Enter`        | Execute selected item          |
| `Shift+Enter`  | Execute without closing Walker |
| `Escape`       | Close Walker                   |
| `↑`/`↓`        | Navigate results               |
| `Tab`          | Next result                    |
| `Shift+Tab`    | Previous result                |
| `Ctrl+E`       | Toggle exact search            |
| `Ctrl+R`       | Resume last query (service only)|

See [Keybindings](/docs/keybindings) for complete list and customization.

## Configuration Tips

Edit `~/.config/walker/config.toml` to customize Walker:

### Change Theme

```toml
theme = "default"  # or your custom theme name
```

### Customize Placeholders

```toml
[placeholders]
"default" = { input = "Search...", list = "No Results" }
"desktopapplications" = { input = "Launch App", list = "No Apps Found" }
```

### Adjust Default Providers

```toml
[providers]
default = [
  "desktopapplications",
  "calc",
  "runner",
  "menus",
  "websearch",
]
empty = ["desktopapplications"]  # Shown when query is empty
max_results = 50
```

See [Configuration](/docs/configuration) for detailed options.

## Common Issues

### Walker Opens but Shows Nothing

**Cause:** Elephant isn't running or no providers are installed.

**Solution:**
```bash
# Check Elephant status
systemctl --user status elephant.service

# List installed providers
elephant providers list

# Install basic providers
yay -S elephant-desktopapplications elephant-providerlist
```

### Walker is Slow to Start

**Solution:** Run Walker as a service (see above).

### Can't Find Applications

**Cause:** Application cache might be outdated.

**Solution:**
1. Open Walker
2. Type `clear applications cache` and run it
3. Or delete `~/.cache/walker/applications.json`

## Next Steps

- [Configuration Guide](/docs/configuration) - Learn all configuration options
- [Keybindings](/docs/keybindings) - Customize keyboard shortcuts
- [Theming](/docs/theming) - Customize Walker's appearance
- [Providers](/docs/providers) - Learn about all available providers
- [Provider Actions](/docs/provider-actions) - Advanced provider interactions
