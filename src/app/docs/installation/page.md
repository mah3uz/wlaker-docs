---
title: Installation
nextjs:
  metadata:
    title: Installation
    description: Install Walker, run it the first time, and learn the basic usage and configuration.
---

This guide gets you running Walker and customizing it in minutes.

## Requirements

- gtk4-layer-shell

## Install

### Arch Linux

```bash
sudo pacman -S walker

// or to install using yay
yay -S walker-bin

// or to build from source
yay -S walker
```

### Building from source

**_Building can take quite a while, be patient_**

Make sure you have the following dependencies installed:

- go
- gtk4
- gtk4-layer-shell
- gobject-introspection
- libvips
- libvips-dev

If building doesn't work, or you are notified with a "package not found" error, please consider installing the developer packages (if available from your package manager):

- gtk4-devel
- gobject-introspection-devel
- graphene-devel
- gtk4-layer-shell-devel

```bash
git clone https://github.com/abenz1267/walker /tmp/walker
cd /tmp/walker/cmd
go build -x -o walker // the '-x' is for debug output
sudo cp walker /usr/bin/
```

Without these you won't be able to build.

### Nix/NixOS

You have two options of installing walker using Nix.

1.  Using the package exposed by this flake

    1. Add to your flake `inputs.walker.url = "github:abenz1267/walker";`
    2. Add `inputs.walker.packages.<system>.default` to `environment.systemPackages` or `home.packages`

2.  Using the home-manager module exposed by this flake:
    1. Add to your flake `inputs.walker.url = "github:abenz1267/walker";`
    2. Add `imports = [inputs.walker.homeManagerModules.default];` into your home-manager config
    3. Configure walker using:

```nix
programs.walker = {
  enable = true;
  runAsService = true;

  # All options from the config.json can be used here.
  config = {
    search.placeholder = "Example";
    ui.fullscreen = true;
    list = {
      height = 200;
    };
    websearch.prefix = "?";
    switcher.prefix = "/";
  };

  # If this is not set the default styling is used.
  theme.style = ''
    * {
      color: #dcd7ba;
    }
  '';
};
```

Additionally, there is a binary caches at `https://walker.cachix.org` and `https://walker-git.cachix.org` which you can use with the following:

```nix
nix.settings = {
  substituters = ["https://walker.cachix.org"];
  trusted-public-keys = ["walker.cachix.org-1:fG8q+uAaMqhsMxWjwvk0IMb4mFPFLqHjuvfwQxE4oJM="];
};
```

```nix
nix.settings = {
  substituters = ["https://walker-git.cachix.org"];
  trusted-public-keys = ["walker-git.cachix.org-1:vmC0ocfPWh0S/vRAQGtChuiZBTAe4wiKDeyyXM0/7pM="];
};
```
---

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

---

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
