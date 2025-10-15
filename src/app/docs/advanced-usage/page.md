---
title: Advanced Usage
nextjs:
  metadata:
    title: Advanced Usage
    description: Advanced features, tips, and tricks for power users of Walker.
---

This guide covers advanced features and use cases for Walker.

## Table of Contents

- [Provider Sets](#provider-sets)
- [Dmenu Mode](#dmenu-mode)
- [Service Mode](#service-mode)
- [Socket Communication](#socket-communication)
- [Custom Menus](#custom-menus)
- [Window Manager Integration](#window-manager-integration)
- [Performance Optimization](#performance-optimization)
- [Scripting and Automation](#scripting-and-automation)
- [Debugging](#debugging)

## Provider Sets

Provider sets allow you to create custom launcher configurations for different workflows.

### Defining Provider Sets

Edit `~/.config/walker/config.toml`:

```toml
[providers.sets.dev]
default = ["runner", "files", "desktopapplications"]
empty = ["files"]

[providers.sets.web]
default = ["websearch", "desktopapplications"]
empty = ["websearch"]

[providers.sets.productivity]
default = ["desktopapplications", "todo", "clipboard"]
empty = ["todo"]
```

### Launching Provider Sets

```bash
walker -s dev          # Development workflow
walker -s web          # Web browsing workflow
walker -s productivity # Productivity workflow
```

### Use Cases

- **Development:** Files, runner, applications
- **Writing:** Applications, clipboard, symbols
- **System Management:** Runner, files, Bluetooth
- **Quick Launcher:** Only applications

## Dmenu Mode

Walker can function as a dmenu replacement, reading from stdin and outputting selected items.

### Basic Usage

```bash
echo -e "Option 1\nOption 2\nOption 3" | walker --dmenu
```

### Streaming Support

For large datasets, stream data to Walker:

```bash
find /home -type f | walker --dmenu
```

### With Custom Prompt

```bash
cat list.txt | walker --dmenu --prompt "Select file:"
```

### Active Item

Highlight a specific item as active:

```bash
echo -e "Item 1\nItem 2\nItem 3" | walker --dmenu --active "Item 2"
```

### Index Output

Output the selected index instead of text:

```bash
echo -e "Option 1\nOption 2\nOption 3" | walker --dmenu -i
# Returns: 0, 1, or 2
```

### Scripting Example

```bash
#!/bin/bash
options="Shutdown\nReboot\nLogout\nSuspend"
choice=$(echo -e "$options" | walker --dmenu --prompt "Power:")

case "$choice" in
  "Shutdown") systemctl poweroff ;;
  "Reboot") systemctl reboot ;;
  "Logout") hyprctl dispatch exit ;;
  "Suspend") systemctl suspend ;;
esac
```

### Integration with Tools

**iwmenu (WiFi management):**
```bash
iwmenu --dmenu="walker --dmenu"
```

**bzmenu (Bluetooth management):**
```bash
bzmenu --dmenu="walker --dmenu"
```

## Service Mode

Running Walker as a service dramatically improves startup performance.

### Starting Service

```bash
walker --gapplication-service
```

### Auto-start Options

#### Systemd User Service

Create `~/.config/systemd/user/walker.service`:

```ini
[Unit]
Description=Walker Application Launcher Service
PartOf=graphical-session.target

[Service]
ExecStart=/usr/bin/walker --gapplication-service
Restart=on-failure
RestartSec=5

[Install]
WantedBy=default.target
```

Enable and start:

```bash
systemctl --user enable --now walker.service
```

#### Hyprland

Add to `~/.config/hypr/hyprland.conf`:

```bash
exec-once=walker --gapplication-service
```

#### i3/Sway

Add to config:

```bash
exec walker --gapplication-service
```

### Service Benefits

- **Instant startup:** No initialization delay
- **Background indexing:** Applications and files indexed in background
- **Resume last query:** `Ctrl+R` resumes previous search (service only)
- **Resource efficiency:** Single process serves all invocations

### Service Management

```bash
# Check status
systemctl --user status walker.service

# Restart service
systemctl --user restart walker.service

# Stop service
systemctl --user stop walker.service

# View logs
journalctl --user -u walker.service -f
```

## Socket Communication

For even faster launching when Walker service is running.

### Using Socket

```bash
nc -U /run/user/1000/walker/walker.sock
```

### Window Manager Keybinding

**Hyprland:**
```bash
bind = SUPER, SPACE, exec, nc -U /run/user/1000/walker/walker.sock
```

**i3/Sway:**
```bash
bindsym $mod+space exec nc -U /run/user/1000/walker/walker.sock
```

**Note:** Socket launch doesn't support command-line arguments. Use regular `walker` command if you need flags.

### Benefits

- Absolute minimal latency
- No process spawning overhead
- Direct IPC communication

## Custom Menus

Create custom menus using Elephant's menu system.

### Creating a Menu

Menus are defined in Elephant's configuration. See [Elephant documentation](https://github.com/abenz1267/elephant) for details.

### Accessing Menus in Walker

Once created in Elephant, access menus via:

1. **Default providers:** Include in default providers
   ```toml
   [providers]
   default = ["menus", "desktopapplications"]
   ```

2. **Prefix:** Assign a prefix
   ```toml
   [[providers.prefixes]]
   prefix = "+"
   provider = "menus:mymenu"
   ```

### Example Use Cases

- **Bookmarks menu:** Quick access to URLs
- **Projects menu:** Open project directories
- **Scripts menu:** Launch custom scripts
- **System actions:** Power menu, system controls

## Window Manager Integration

### Hyprland Complete Setup

`~/.config/hypr/hyprland.conf`:

```bash
# Start services
exec-once=elephant service enable
exec-once=systemctl --user start elephant.service
exec-once=walker --gapplication-service

# Keybindings
bind = SUPER, SPACE, exec, nc -U /run/user/1000/walker/walker.sock
bind = SUPER, D, exec, walker
bind = SUPER SHIFT, D, exec, walker -s dev
bind = SUPER, R, exec, walker --modules runner
bind = SUPER, F, exec, walker --modules files

# Dmenu replacement
bind = SUPER, P, exec, walker --dmenu
```

### i3/Sway Setup

`~/.config/i3/config` or `~/.config/sway/config`:

```bash
# Start services
exec elephant service enable
exec systemctl --user start elephant.service
exec walker --gapplication-service

# Keybindings
bindsym $mod+space exec nc -U /run/user/1000/walker/walker.sock
bindsym $mod+d exec walker
bindsym $mod+Shift+d exec walker -s dev
bindsym $mod+r exec walker --modules runner
bindsym $mod+f exec walker --modules files

# Dmenu replacement
bindsym $mod+p exec walker --dmenu
```

### Multiple Launch Modes

Set up different keybindings for different contexts:

```bash
# General launcher
SUPER + Space: walker

# Applications only
SUPER + A: walker --modules desktopapplications

# Files only
SUPER + F: walker --modules files

# Command runner
SUPER + R: walker --modules runner

# Clipboard
SUPER + V: walker --modules clipboard

# Web search
SUPER + W: walker --modules websearch
```

## Performance Optimization

### 1. Run as Service

Always run Walker as a service for best performance:

```bash
walker --gapplication-service &
```

### 2. Limit Results

Reduce max results for faster rendering:

```toml
[providers]
max_results = 30

[providers.max_results_provider]
desktopapplications = 15
files = 20
```

### 3. Disable Mouse

If you only use keyboard:

```toml
disable_mouse = true
```

### 4. Optimize Provider Selection

Only query providers you need:

```toml
[providers]
default = ["desktopapplications", "calc"]  # Minimal set
empty = ["desktopapplications"]
```

### 5. Provider-Specific Settings

Some providers have performance settings in Elephant's config. Check Elephant documentation.

## Scripting and Automation

### Launch Specific Modules

```bash
walker --modules applications,runner,calc
```

### Launch with Provider Set

```bash
walker -s myset
```

### Dmenu Integration

```bash
# Window switcher
hyprctl clients -j | jq -r '.[].title' | walker --dmenu
```

### Automation Examples

**Quick todo entry:**
```bash
#!/bin/bash
todo=$(echo "" | walker --dmenu --prompt "New todo:")
if [ -n "$todo" ]; then
  echo "!$todo" | walker --dmenu
fi
```

**Project launcher:**
```bash
#!/bin/bash
project=$(find ~/projects -maxdepth 1 -type d | walker --dmenu)
if [ -n "$project" ]; then
  cd "$project" && code .
fi
```

## Debugging

### Enable Debug Mode

```toml
debug = true
```

Or run with flag:

```bash
walker --debug
```

### Check Elephant Connection

```bash
# Verify Elephant is running
systemctl --user status elephant.service

# Check Elephant providers
elephant providers list
```

### View Logs

**Walker logs:**
```bash
# If running as service
journalctl --user -u walker.service -f

# If running manually, check terminal output
```

**Elephant logs:**
```bash
journalctl --user -u elephant.service -f
```

### Common Issues

**Walker shows "Waiting for elephant..."**
- Elephant isn't running
- Elephant crashed
- Connection issue

**No results appearing**
- No providers installed
- Providers not configured in Elephant
- Provider cache outdated

**Slow performance**
- Not running as service
- Too many providers queried
- Large result sets

**Keybindings not working**
- Check for conflicts
- Enable debug mode to see keybind events
- Verify keybind syntax in config

### Reset Configuration

```bash
# Backup current config
mv ~/.config/walker ~/.config/walker.backup

# Walker will create fresh config on next launch
walker
```

## Advanced Configuration Patterns

### Context-Aware Setup

Different configs for different contexts:

```bash
# Work profile
walker --config ~/.config/walker/work.toml

# Personal profile
walker --config ~/.config/walker/personal.toml
```

### Dynamic Provider Selection

Script to choose providers based on context:

```bash
#!/bin/bash
hour=$(date +%H)

if [ $hour -ge 9 ] && [ $hour -le 17 ]; then
  # Work hours: productivity tools
  walker -s work
else
  # Off hours: entertainment
  walker -s personal
fi
```

### Conditional Theming

Use different themes based on time or context:

```bash
#!/bin/bash
if [ $(date +%H) -ge 18 ]; then
  sed -i 's/theme = .*/theme = "dark"/' ~/.config/walker/config.toml
else
  sed -i 's/theme = .*/theme = "light"/' ~/.config/walker/config.toml
fi
walker
```

## Best Practices

1. **Run as service:** Always use service mode for daily use
2. **Use provider sets:** Create sets for different workflows
3. **Limit results:** Keep max_results reasonable (30-50)
4. **Organize providers:** Use prefixes effectively
5. **Regular cleanup:** Clear caches periodically
6. **Monitor performance:** Check if providers are slow
7. **Update regularly:** Keep Walker and Elephant updated
8. **Backup config:** Version control your config files
