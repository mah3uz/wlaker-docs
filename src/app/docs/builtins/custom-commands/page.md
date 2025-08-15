---
title: Custom Commands
nextjs:
  metadata:
    title: Custom Commands
    description: Create your own commands with names, icons, terminals, and alternate actions.
---

Define your own launchers with names, icons, and terminal support.

## Configure

```toml
[builtins.custom_commands]
name = "custom_commands"
icon = "utilities-terminal"
placeholder = "Custom Commands"

[[builtins.custom_commands.commands]]
name = "Edit config"
icon = "accessories-text-editor"
cmd = 'xdg-open ~/.config/walker/config.toml'

[[builtins.custom_commands.commands]]
name = "Update system"
cmd = 'sudo pacman -Syu'
terminal = true

[[builtins.custom_commands.commands]]
name = "Open projects"
cmd = 'xdg-open ~/Projects'
terminal_title_flag = "--title"
```

You can set `env`, `path`, and `cmd_alt` as needed.
