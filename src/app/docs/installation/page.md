---
title: Installation
nextjs:
  metadata:
    title: Installation
    description: Install Walker, run it the first time, and learn the basic usage and configuration.
---

This guide covers installing Walker and its required dependencies.

## Prerequisites

### Required Dependencies

1. **Elephant** - The backend service that Walker depends on
   - Walker cannot function without Elephant running
   - [Elephant GitHub Repository](https://github.com/abenz1267/elephant)

2. **GTK4** (version 4.6+)
3. **gtk4-layer-shell** - For Wayland layer-shell support
4. **Protocol Buffers compiler** - For gRPC communication
5. **cairo** - Graphics library
6. **poppler-glib** - PDF rendering support

## Installation Methods

### Arch Linux

Walker is available in the AUR:

```bash
# Install pre-built binary
yay -S walker

# Or build from source
yay -S walker-git
```

You'll also need to install Elephant:

```bash
yay -S elephant
```

### Building from Source

#### Install Build Dependencies

```bash
# Dependencies needed for building
- GTK4 development files
- gtk4-layer-shell development files
- Protocol Buffers compiler (protoc)
- cairo development files
- poppler-glib development files
- Rust toolchain (via rustup)
```

#### Build Steps

```bash
# Clone the repository
git clone https://github.com/abenz1267/walker.git
cd walker

# Build with Cargo
cargo build --release

# Install the binary
sudo cp target/release/walker /usr/local/bin/

# Copy default configuration
mkdir -p ~/.config/walker
cp resources/config.toml ~/.config/walker/
```

### Nix/NixOS

Walker can be installed via Nix flakes with two approaches:

#### Option 1: Using the Flake Package

Add Walker to your flake inputs:

```nix
{
  inputs = {
    elephant.url = "github:abenz1267/elephant";
    walker = {
      url = "github:abenz1267/walker";
      inputs.elephant.follows = "elephant";
    };
  };
}
```

Then add to your packages:

```nix
# System-wide
environment.systemPackages = [ inputs.walker.packages.<system>.default ];

# Or user-level (Home Manager)
home.packages = [ inputs.walker.packages.<system>.default ];
```

#### Option 2: Using Home Manager Module

Import the Home Manager module:

```nix
imports = [ inputs.walker.homeManagerModules.default ];

programs.walker = {
  enable = true;
  runAsService = true;

  # Configuration options
  config = {
    theme = "default";
    placeholders.default = {
      input = "Search";
      list = "No Results";
    };
    providers.prefixes = [
      { provider = "websearch"; prefix = "+"; }
      { provider = "providerlist"; prefix = "_"; }
    ];
    keybinds.quick_activate = ["F1" "F2" "F3"];
  };

  # Custom theme
  themes = {
    "my-theme" = {
      style = ''
        /* Your CSS here */
      '';
      layouts = {
        "layout" = ''<!-- Your XML layout -->'';
      };
    };
  };
};
```

#### Nix Binary Cache

Speed up builds by using the Walker binary cache:

```nix
nix.settings = {
  extra-substituters = [
    "https://walker.cachix.org"
    "https://walker-git.cachix.org"
  ];
  extra-trusted-public-keys = [
    "walker.cachix.org-1:fG8q+uAaMqhsMxWjwvk0IMb4mFPFLqHjuvfwQxE4oJM="
    "walker-git.cachix.org-1:vmC0ocfPWh0S/vRAQGtChuiZBTAe4wiKDeyyXM0/7pM="
  ];
};
```

## Post-Installation

### 1. Start Elephant Service

Walker requires Elephant to be running:

```bash
# Start Elephant as a user service
elephant service enable
systemctl --user start elephant.service

# Or start manually
elephant
```

### 2. Install Elephant Providers

You need to install at least some providers for Elephant:

```bash
# Essential providers
yay -S elephant-providerlist        # Provider switcher
yay -S elephant-desktopapplications  # Desktop applications

# Optional providers
yay -S elephant-files               # File browser
yay -S elephant-runner              # Command runner
yay -S elephant-calc                # Calculator
yay -S elephant-websearch           # Web search
yay -S elephant-clipboard           # Clipboard history
yay -S elephant-symbols             # Symbol picker
```

For other distributions, check the [Elephant documentation](https://github.com/abenz1267/elephant).

### 3. First Run

```bash
walker
```

This will:
- Create default configuration at `~/.config/walker/config.toml`
- Create default theme files in `~/.config/walker/themes/`

## Running as a Service

For faster startup, run Walker as a background service:

```bash
walker --gapplication-service
```

Then open Walker anytime with:

```bash
walker
```

Or use the socket for even faster launch (requires `openbsd-netcat`):

```bash
nc -U /run/user/1000/walker/walker.sock
```

Note: The socket method doesn't support command-line options.

## Troubleshooting

### Walker won't start

1. **Check if Elephant is running:**
   ```bash
   systemctl --user status elephant.service
   ```

2. **Verify providers are installed:**
   ```bash
   elephant providers list
   ```

3. **Check Walker logs:**
   ```bash
   walker --debug
   ```

### Missing dependencies

If you get errors about missing libraries:

```bash
# Arch Linux
sudo pacman -S gtk4 gtk4-layer-shell cairo poppler-glib protobuf

# Fedora
sudo dnf install gtk4 gtk4-layer-shell cairo poppler-glib protobuf-compiler

# Ubuntu/Debian (may need PPA for GTK4)
sudo apt install libgtk-4-dev libgtk4-layer-shell-dev libcairo2-dev libpoppler-glib-dev protobuf-compiler
```

## Next Steps

- [Getting Started](/docs/getting-started) - Learn basic usage
- [Configuration](/docs/configuration) - Customize Walker to your needs
- [Keybindings](/docs/keybindings) - Set up keyboard shortcuts
