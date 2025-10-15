---
title: Providers
nextjs:
  metadata:
    title: Providers
    description: Learn about all available providers and their features in Walker.
---

Providers are plugins for Elephant that supply data to Walker. Each provider serves a specific purpose, from launching applications to managing clipboard history.

## Available Providers

### Desktop Applications

**Provider:** `desktopapplications`
**Prefix:** None (default) or configure custom prefix
**Package:** `elephant-desktopapplications`

Launches installed GUI applications from `.desktop` files.

**Features:**
- Searches application names, descriptions, and keywords
- Desktop actions support (e.g., "New Private Window" for Firefox)
- History-aware ranking (frequently used apps appear higher)
- Context-aware (prioritizes apps with open windows)
- Pinning support (pin favorite apps to the top)
- Auto-detects newly installed applications

**Usage:**
```text
firefox
code
obs
```

**Actions:**
- Start application
- Start and keep Walker open
- Pin/unpin application
- Reorder pinned applications

### Calculator

**Provider:** `calc`
**Prefix:** `=`
**Package:** `elephant-calc`

Performs mathematical calculations using libqalculate.

**Features:**
- Basic arithmetic operations
- Scientific functions
- Unit conversions
- Currency conversion (with exchange rates)
- History of calculations
- Save frequently used calculations

**Usage:**
```text
=2 + 2
=(100 * 1.19) - 5
=50 km to miles
=100 USD to EUR
=sin(45)
```

**Actions:**
- Copy result
- Delete from history
- Save calculation

### Command Runner

**Provider:** `runner`
**Prefix:** `>`
**Package:** `elephant-runner`

Executes shell commands and scripts.

**Features:**
- Parses shell config for aliases
- Lists all binaries in PATH
- Exclusive list mode or all binaries
- Ignore list for unwanted commands
- Smart matching: `shu now` → `shutdown now`
- Command history

**Usage:**
```text
>htop
>systemctl status
>git status
>docker ps
```

**Actions:**
- Run command
- Run in terminal

### File Browser

**Provider:** `files`
**Prefix:** `/`
**Package:** `elephant-files`

Browse and open files and directories.

**Features:**
- Fast fuzzy file search
- Navigate directory tree
- Open files with default applications
- Drag & drop support
- Copy file or file path

**Usage:**
```text
/home/user/Documents
/etc/nginx/nginx.conf
/var/log
```

**Actions:**
- Open file
- Open parent directory
- Copy file path
- Copy file

### Web Search

**Provider:** `websearch`
**Prefix:** `@`
**Package:** `elephant-websearch`

Search the web using configured search engines.

**Features:**
- Multiple search engines (Google, DuckDuckGo, Ecosia, Yandex)
- Custom search engines
- Direct website opening (detects URLs)

**Usage:**
```text
@rust programming
@github walker
@https://example.com
```

**Actions:**
- Open in default browser

### Clipboard History

**Provider:** `clipboard`
**Prefix:** `:`
**Package:** `elephant-clipboard`

Access clipboard history with text and images.

**Features:**
- Stores clipboard history
- Image clipboard support
- Timestamped entries
- Search clipboard content
- Edit clipboard entries
- Toggle image display

**Usage:**
```text
:
```

Then search your clipboard history.

**Actions:**
- Copy to clipboard
- Remove entry
- Clear all history
- Toggle image display
- Edit entry

### Symbol Picker

**Provider:** `symbols`
**Prefix:** `.`
**Package:** `elephant-symbols`

Insert special symbols and characters.

**Features:**
- Large collection of symbols
- Search by name or symbol
- Categories: arrows, math, currency, etc.

**Usage:**
```text
.arrow
.check
.copy
.lambda
```

**Actions:**
- Insert symbol (copies to clipboard or types it)

### Unicode

**Provider:** `unicode`
**Package:** `elephant-unicode`

Search and insert Unicode characters.

**Features:**
- Complete Unicode database
- Search by character name
- Search by code point

**Usage:**
```text
greek alpha
emoji cat
mathematical bold
```

**Actions:**
- Insert character

### Provider List / Switcher

**Provider:** `providerlist`
**Prefix:** `;`
**Package:** `elephant-providerlist`

Switch between available providers.

**Features:**
- Lists all installed providers
- Quick provider switching
- Shows provider descriptions

**Usage:**
```text
;
```

Then select a provider to switch to it exclusively.

**Actions:**
- Activate provider

### Todo List

**Provider:** `todo`
**Prefix:** `!`
**Package:** `elephant-todo`

Simple todo list with time tracking.

**Features:**
- Create and manage todos
- Mark todos as active/inactive/done
- Time tracking
- Scheduling with notifications
- Search todos

**Usage:**
```text
!buy groceries
!call dentist tomorrow
```

**Actions:**
- Save todo
- Delete todo
- Mark active/inactive
- Mark as done
- Clear completed todos

### SSH

**Provider:** `ssh`
**Package:** `elephant-ssh`

Connect to SSH hosts from your config.

**Features:**
- Parses `~/.ssh/config`
- Parses `~/.ssh/known_hosts`
- Quick SSH connections

**Usage:**
```text
myserver
user@host
```

**Actions:**
- Connect via SSH (opens terminal)

### Bookmarks

**Provider:** `bookmarks`
**Package:** `elephant-bookmarks`

Access custom bookmarks.

**Features:**
- Custom bookmark management
- Quick access to URLs
- Browser bookmark support (planned)

**Actions:**
- Open bookmark

### Emojis

**Provider:** `emojis`
**Package:** `elephant-emojis`

Search and insert emojis.

**Features:**
- Complete emoji database
- Search by name or keyword
- Categories and skin tones

**Usage:**
```text
smile
heart
fire
```

**Actions:**
- Insert emoji

### Bluetooth

**Provider:** `bluetooth`
**Package:** `elephant-bluetooth`

Manage Bluetooth devices.

**Features:**
- List paired devices
- Connect/disconnect devices
- Pair new devices
- Trust/untrust devices
- Remove devices
- Device scanning

**Actions:**
- Connect/disconnect
- Pair device
- Trust/untrust
- Remove device
- Scan for devices

### Arch Linux Packages

**Provider:** `archlinuxpkgs`
**Package:** `elephant-archlinuxpkgs`

Search and manage Arch Linux packages (official + AUR).

**Features:**
- Search official repos and AUR
- Install packages
- Remove packages
- List exclusively installed packages

**Actions:**
- Install package
- Remove package

### Hyprland Keybinds

**Provider:** `hyprlandkeybinds`
**Package:** `elephant-hyprlandkeybinds`

Browse and execute Hyprland keybindings.

**Features:**
- Parses Hyprland config
- Shows all configured keybinds
- Execute keybind via hyprctl

**Actions:**
- Execute keybind

### Windows

**Provider:** `windows`
**Package:** `elephant-windows`

Window switcher for your desktop.

**Features:**
- List open windows
- Switch to window
- Workspace-aware (if supported)

**Actions:**
- Focus window

### Translation

**Provider:** `translation`
**Package:** `elephant-translation`

Translate text between languages.

**Features:**
- Uses Google Translate (free API)
- Auto-detect source language
- Multiple target languages

**Usage:**
```bash
hello world | es
bonjour | en
```

**Actions:**
- Copy translation

### Commands (Walker Commands)

**Provider:** `commands`
**Package:** Built-in

Internal Walker commands.

**Features:**
- Clear application cache
- Clear clipboard history
- Reload configuration
- Other utility commands

**Usage:**
```bash
clear applications cache
clear clipboard
```

### Custom Commands

**Provider:** `customcommands`
**Package:** `elephant-customcommands`

Define and run custom one-off commands.

**Features:**
- Define commands in config
- Quick access to rarely-used commands
- No need for separate keybindings

**Example config:**
```toml
[customcommands]
"toggle window floating" = "hyprctl dispatch togglefloating"
"reload waybar" = "killall waybar && waybar &"
```

### XDG Desktop Portal Hyprland Share Picker

**Provider:** `xdphpicker`
**Package:** `elephant-xdphpicker`

Select windows/monitors/regions for screen sharing.

**Features:**
- Select window to share
- Select monitor to share
- Select region to share
- Integrates with xdg-desktop-portal-hyprland

### Menus

**Provider:** `menus`
**Prefix:** Custom (define in config)

Custom menus created with Elephant.

**Features:**
- Create custom menus via Elephant
- Display in Walker
- Flexible menu structure
- Custom actions per menu item

**Usage:**
You create menus in Elephant, then access them via Walker.

Example prefix config:
```toml
[[providers.prefixes]]
prefix = "+"
provider = "menus:mymenu"
```

## Installing Providers

Providers are separate packages that must be installed:

### Arch Linux (AUR)

```bash
# Essential
yay -S elephant-providerlist elephant-desktopapplications

# Commonly used
yay -S elephant-files elephant-runner elephant-calc elephant-websearch

# Optional
yay -S elephant-clipboard elephant-symbols elephant-unicode
yay -S elephant-emojis elephant-bluetooth elephant-archlinuxpkgs
```

### Other Distributions

Check the [Elephant documentation](https://github.com/abenz1267/elephant) for installation on other distributions.

### Building from Source

Each provider can be built from source. See provider-specific repositories.

## Configuring Providers

### Default Providers

Set which providers are queried by default:

```toml
[providers]
default = [
  "desktopapplications",
  "calc",
  "runner",
  "menus",
  "websearch",
]
```

### Empty Query Providers

Providers shown when search is empty:

```toml
[providers]
empty = ["desktopapplications"]
```

### Provider Prefixes

Assign prefixes for quick access:

```toml
[[providers.prefixes]]
prefix = ";"
provider = "providerlist"

[[providers.prefixes]]
prefix = ">"
provider = "runner"

[[providers.prefixes]]
prefix = "/"
provider = "files"
```

### Max Results

Limit results per provider:

```toml
[providers]
max_results = 50  # Global default

[providers.max_results_provider]
desktopapplications = 20
files = 30
runner = 50
```

## Provider Sets

Create custom sets of providers for different workflows:

```toml
[providers.sets.dev]
default = ["runner", "files", "desktopapplications"]
empty = ["files"]

[providers.sets.web]
default = ["websearch", "bookmarks", "desktopapplications"]
empty = ["bookmarks"]
```

Launch a set:

```bash
walker -s dev
walker -s web
```

## Elephant Configuration

Some providers have additional configuration in Elephant's config file (`~/.config/elephant/config.toml`). See Elephant documentation for provider-specific options.

## Next Steps

- [Provider Actions](/docs/provider-actions) - Detailed action reference
- [Configuration](/docs/configuration) - Configure providers
- [Getting Started](/docs/getting-started) - Learn basic usage
