---
title: SSH
nextjs:
  metadata:
    title: SSH
    description: List SSH hosts from your config and connect quickly with history support.
---

List SSH hosts from config files and connect to them.

## Configure

```toml
[builtins.ssh]
name = "ssh"
icon = "preferences-system-network"
placeholder = "SSH"
switcher_only = true
history = true
refresh = true
# config_file = "~/.ssh/config"
# host_file = "~/.ssh/known_hosts"
```

Use history to surface frequently used hosts.
