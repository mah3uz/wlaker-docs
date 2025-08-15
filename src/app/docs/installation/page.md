---
title: Installation
nextjs:
  metadata:
    title: Installation
    description: Install Walker, run it the first time, and learn the basic usage and configuration.
---

This guide gets you running Walker and customizing it in minutes.

## Install

### Arch Linux
`sudo pacman -S walker`

### Nix/NixOS

```nix
# flake input
inputs.walker.url = "github:abenz1267/walker";

# as a package
environment.systemPackages = [ inputs.walker.packages.${system}.walker ];
```

#### Home Manager

```nix
{ inputs, pkgs, ... }:
{
  imports = [ inputs.walker.homeManagerModules.default ];

  programs.walker = {
    enable = true;
    # optional: settings = { theme = "default"; };
  };
}
```

#### NixOS module

```nix
{ inputs, ... }:
{
  imports = [ inputs.walker.nixosModules.default ];

  services.walker = {
    enable = true; # runs walker as a service
  };
}
```

#### Dev shell

```bash
nix develop github:abenz1267/walker
```

See `flake.nix` for full outputs: `packages.walker`, `homeManagerModules.walker`, `nixosModules.walker`.


### Go build

```bash
# prerequisites: wayland, gtk4, gotk4 bindings, wl-clipboard
# on Arch: sudo pacman -S gtk4 wl-clipboard fd ttf-nerd-fonts-symbols

# build and install
make build # or: go build ./cmd
sudo install -Dm755 walker /usr/bin/walker
```



## First run

```bash
walker
```

- Creates a default config at `~/.config/walker/config.toml`.
- Creates default theme files under `~/.config/walker/themes/`.

## Launching as a service (faster)

Run in background so subsequent launches are instant:

```bash
walker --gapplication-service &
# later re-open a window
walker
```

See the Service page for systemd user unit and autostart.

## Basic usage

- Start typing to search across the active module.
- Use `/` to open the Switcher, then pick a module.
- Up/Down to move, Enter to run, Esc to close.
- Tab accepts typeahead suggestions.

## Configure

Edit `~/.config/walker/config.toml`. Each built-in module has a section under `[builtins.*]`. See Configuration and Built-ins pages for examples.

```toml
# ~/.config/walker/config.toml
terminal_title_flag = "--title"
locale = "en_US"
theme = "default"

[builtins.runner]
name = "runner"
placeholder = "Run..."
```
