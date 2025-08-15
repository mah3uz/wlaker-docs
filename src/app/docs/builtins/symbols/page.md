---
title: Symbols
nextjs:
  metadata:
    title: Symbols
    description: Browse common symbols and glyphs and copy them to the clipboard.
---

Common symbols and glyphs. Copy to clipboard with Enter.
---
## Configure

```toml
[builtins.symbols]
name = "symbols"
placeholder = "Symbols"
switcher_only = true
history = true
typeahead = true
exec = "wl-copy '%RESULT%'"
```

Great for quickly grabbing checkmarks, arrows, and math symbols.
title: Service
nextjs:
  metadata:
    title: Service
    description: Run Walker as a background service, set up a systemd user unit, and manage autostart.
---

Run Walker as a background service for instant open.

## Start service

```bash
walker --gapplication-service &
```

Re-open a window anytime:

```bash
walker
```

## Systemd user unit

Example unit (see `assets/walker.service`):

```ini
[Unit]
Description=Walker launcher service
PartOf=graphical-session.target
After=graphical-session.target
Requires=graphical-session.target
ConditionEnvironment=WAYLAND_DISPLAY

[Service]
Type=simple
ExecStart=/usr/bin/walker --gapplication-service
Slice=session.slice
Restart=on-failure

[Install]
WantedBy=graphical-session.target
```

Install and enable:

```bash
mkdir -p ~/.config/systemd/user
cp assets/walker.service ~/.config/systemd/user/
systemctl --user daemon-reload
systemctl --user enable --now walker.service
```

## Autostart helper

Walker can manage a simple autostart `.desktop` for you:

```bash
walker --enableautostart
walker --disableautostart
```
