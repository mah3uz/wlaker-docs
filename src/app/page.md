---
title: Getting started
---

{% callout title="Important: This is not official docs/website!" %}
This site is not officially maintained by the Walker team, but is provided by the community.
It is not guaranteed to be up-to-date or accurate.
{% /callout %}

Learn how to get Walker on your computer and start using. It's free. {% .lead %}

{% quick-links %}

{% quick-link title="Installation" icon="installation" href="/docs/installation" description="Step-by-step guides to setting up your system and installing the library." /%}

{% quick-link title="Getting Started" icon="presets" href="/docs/getting-started" description="Learn how the internals work and contribute." /%}

{% quick-link title="Providers" icon="plugins" href="/docs/providers" description="Extend walker with provider only use what you need." /%}

{% quick-link title="Themes" icon="theming" href="/docs/theming" description="Learn to easily customize and modify your walker's visual design to fit your liking." /%}

{% /quick-links %}

Walker is a highly extendable application launcher that doesn't hold back on features and usability. Fast. Unclutters your brain. Improves your workflow.

---

# Walker

![Walker screenshot](https://raw.githubusercontent.com/mah3uz/wlaker-docs/refs/heads/main/screenshot.png "Walker Screenshot")

Walker is a modern, fast application launcher frontend for Elephant, built with GTK4 and Rust. It provides a clean interface for launching applications, running commands, searching files, and much more.

## Quick Links

- [GitBook Documentation](https://benz.gitbook.io/walker)
- [GitHub Repository](https://github.com/abenz1267/walker)
- [Elephant Repository](https://github.com/abenz1267/elephant)

## What is Walker?

Walker is a launcher frontend that communicates with Elephant, a backend service that provides various data providers. The separation allows for a clean, maintainable architecture where:

- **Elephant** handles all the heavy lifting: searching applications, files, managing clipboard history, etc.
- **Walker** provides the beautiful GTK4 interface for user interaction

## Features
The following Elephant providers are implemented by default:

* **Desktop Applications:** Launch installed GUI applications
* **Calculator:** Perform mathematical calculations with `=` prefix
* **File Browser:** Navigate and open files with `/` prefix
* **Command Runner:** Execute shell commands
* **Websearch:** Search the web with custom-defined engines
* **Clipboard History:** Access clipboard history with : prefix
* **Symbol Picker:** Insert special symbols with `.` prefix
* **Provider List:** Switch between providers with `;` prefix
* **Menu Integration:** Create custom menus with elephant and let walker display them
* **Dmenu:** Your good old dmenu ... with seamless menus!
* **Arch Linux Packages:** Search through available packages (official and aur), install or delete a target! List all exlusively installed packages.
* **Todo List:** create simple todo items with basic time tracking, scheduling and notifications
* **Bluetooth:** basic bluetooth management

## Highlights
- Fast, async result handling
- Multiple data providers (applications, files, calculator, websearch, etc.)
- Highly customizable theming
- Extensive keybinding support
- Provider prefix system for quick access
- Custom action definitions per provider
- Service mode for instant startup
