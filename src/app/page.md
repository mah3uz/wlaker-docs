---
title: Getting started
---

{% callout title="Important: This is not official website!" %}
This site is not officially maintained by the Walker team, but is provided by the community.
It is not guaranteed to be up-to-date or accurate.
{% /callout %}

Learn how to get Walker on your computer and start using. It's free. {% .lead %}

{% quick-links %}

{% quick-link title="Installation" icon="installation" href="/docs/installation" description="Step-by-step guides to setting up your system and installing the library." /%}

{% quick-link title="Architecture guide" icon="presets" href="https://github.com/abenz1267/walker/wiki" description="Learn how the internals work and contribute." /%}

{% quick-link title="Plugins" icon="plugins" href="/docs/plugins" description="Extend walker with third-party plugins or write your own." /%}

{% quick-link title="Themes" icon="theming" href="/docs/themes-and-layouts" description="Learn to easily customize and modify your walker's visual design to fit your brand." /%}

{% /quick-links %}

Walker is a highly extendable application launcher that doesn't hold back on features and usability. Fast. Unclutters your brain. Improves your workflow.

---

## Quick start

{% callout type="warning" title="You should know!" %}
Walker is currently undergoing a much-needed rewrite in order to release a `1.0.0`.

The latest functional version can be found in the [0.13.26-branch](https://github.com/abenz1267/walker/tree/0.13.26).
{% /callout %}

---

## Features

- plugin support: simple stdin/stdout (external or via configuration, see wiki)
- icons/images
- start as service for faster startup
- run entries via labels (F<1-8> or jkl;asdf)
- non-blocking async handling of results
- typeahead
- start with explicit modules, style or config
- drag&drop support
- dmenu-mode (with streaming support for large datasets)
- run as password input
- theming support (global, per module, with inheritance)

## Builtin Modules

- ai
    - anthropic (Claude 3.5), gemini (gemini-2.0-flash)
    - define different prompts
- runner
    - parses your shell config for aliases
    - exclusive list or all binaries
    - ignore-list
    - generic runner
    - semi-smart: `shu now` => `shutdown now`
- translation
    - currently only free google translate
- windows
    - simple window switcher
- desktop applications
    - history-aware
    - desktop actions (f.e. `Open a new private window` [Firefox])
    - puts newly installed applications on top
    - context-aware (context = open windows)
- websearch
    - simple websearch
    - google, duckduckgo, ecosia, yandex
    - can open websites directly
- clipboard
    - simple clipboard history
    - with images
- module switcher
    - lets you switch to specific modules
- commands (for Walker, f.e. clear cache)
- ssh
    - parses your `known_hosts` and `config` files
- finder
    - simple fuzzy finder
    - drag&drop support
- emojis
- symbols
- bookmarks
    - currently custom bookmarks only
    - planned: bookmarks from browsers
- calculator
    - uses [libqalculate](https://github.com/Qalculate/libqalculate)
- custom commands (for running simple commands)
    - lets you define and run simple one-off commands
    - f.e. `toggle window floating`
    - no need to create keybinds for commands you don't run often
- xdg-desktop-portal-hyprland share picker
    - lets you select windows/monitors/region for sharing
- hyprland keybinds
    - parses your hyprland config for keybinds
    - shows the keybind
    - execute the keybind via hyprctl

## Compatible tools

- [iwmenu](https://github.com/e-tho/iwmenu) - lets you manage Wi-Fi through dmenu mode
- [bzmenu](https://github.com/e-tho/bzmenu) - lets you manage Bluetooth through dmenu mode

## Requirements

- gtk4-layer-shell

## Installation

```bash
arch:
yay -S walker-bin

// or to build from source
yay -S walker
```

--- 

## Running as a service

This depends on your system:

Option 1: Autostart Walker with `walker --gapplication-service` and it will run in the background.

Option 2: You can let Walker create an autostart desktop file for you by running `walker --enableautostart`.

Then just run `walker` to bring it up.
You can also send re-open walker by calling the socket at `/tmp/walker-reopen.sock`. F.e. with `nc -U /tmp/walker-reopen.sock`.

Example for Hyprland:

```bash
exec-once=walker --gapplication-service
```

## Config & Style

[Check configuration guide](/docs/configuration) for more information on how to configure Walker.

## Start Walker with explicit modules

You can start walker with explicit modules by using the `--modules` flag. F.e:

```bash
walker --modules applications,ssh
```

Will tell Walker to only use the applications and ssh module.

## Styling with typeahead enabled

If you have typeahead enabled, make sure that your `#search` has no background, so the typeahead is readable.

## Providing your own modules

If you want to extend walker with your own modules, you can do that in the config.

```toml
[[plugins]]
prefix = "!"
name = "mymodule"
src = "node /path/to/myscript.js"
```

See the wiki for more information.

### Dynamic Styling

The window and items will have a class based on the source. Selecting an item will change the windows class to the current selections source. Using a prefix will apply that sources classes to the window.

F.e. search = `!somecommand` => `#window.runner`

| class                | condition                  |
| -------------------- | -------------------------- |
| `#window.activation` | AM enabled                 |
| `#spinner.visible`   | Processing in progress     |
| `#item.<entryclass>` | Always                     |
| `#item.active`       | Dmenu with '--active'-flag |

### Starting as service

Start with `walker --gapplication-service` to start in service-mode. Calling `walker` normally afterwards should be rather fast.

### Additional flags

`walker --help`

## Keybinds

The keybinds are customizable, check the wiki.

AM = Activation Mode

| Key                                                                     | Description                                                              |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| `Enter`                                                                 | activate selection                                                       |
| `Alt+Enter`                                                             | activate selection with alternative command. By default: run in terminal |
| `Shift+Enter`                                                           | activate selection without closing                                       |
| `Ctrl+j` (if ActivationMode is disabled), `Down`, `Tab`                 | next entry                                                               |
| `Ctrl+k` (if ActivationMode is disabled), `Up`, `LEFT_TAB` (shift+tab?) | previous entry                                                           |
| `Escape`                                                                | close                                                                    |
| `Ctrl + Label`                                                          | Activate item by label                                                   |
| `Ctrl + c`                                                              | AI: copy last response                                                   |
| `Ctrl + r`                                                              | All (service-only): resume last query,AI: resume last session for prompt |
| `Ctrl + x`                                                              | AI: clear current session                                                |
| `Ctrl + e`                                                              | AI: run last message in terminal                                         |
| `Ctrl + m`                                                              | toggle exact match search                                                |
| `Ctrl + Shift + Label`                                                  | Activate item by label without closing                                   |
| `Shift+Backspace`                                                       | All: delete entry from history, Clipboard: remove from clipboard         |

### Activation Mode

Activation-Mode can be triggered by holding `LCtrl` ( or `LAlt`). The window will get an additional class `activation` you can use for styling. While activated, you can run items by pressing their respective label. This only works for the top 8 items.

## FAQ

### Newly installed or removed applications aren't shown / are still shown

Make sure to clean the applications cache by either running the "Clear Applications Cache" command from within Walker (using the `commands` module) or by deleting the `applications.json` file in `$HOME/.cache/walker/`.

Additionally you can disable the cache completely by setting

```toml
[applications]
cache = false
```

in your config.

### Applications launched via Walker close if the systemd-service stops

Look [here](https://github.com/abenz1267/walker/issues/331#issuecomment-3031539042).

My personal recommendation is to start the Walker service as an xdg-autostart application. That's up to you though.