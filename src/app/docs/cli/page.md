---
title: CLI
nextjs:
  metadata:
    title: CLI
    description: Command-line flags for service mode, dmenu compatibility, theming, and behavior overrides.
---

Walker exposes a CLI with flags for running as a service, dmenu mode, theming, and behavior overrides.

## Usage

```bash
walker [OPTIONS]
```

## Common options

- --version (-v): print version
- --new (-n): force a new instance (don’t reuse service)
- --modules (-m) "mod1,mod2": explicitly load modules only
- --theme (-s) name: pick a theme for this run
- --placeholder (-p) text: set search placeholder
- --query (-q) text: set initial query
- --width (-w) N: override width
- --height (-h) N: override height
- --autoselect (-x): auto-activate single item
- --keepsort (-k): don’t sort alphabetically
- --password (-y): password mode (hides input)
- --forceprint (-f): print input if no item selected
- --clear-clipboard (-u): clear clipboard storage
- --createuserconfig (-C): write default config+theme to user dir
- --enableautostart (-A) / --disableautostart (-D): manage user autostart
- --dmenu (-d): dmenu compatibility mode (see below)

## Dmenu mode

Read options and entries from stdin, with compatibility flags:

- --separator (-t) char: column separator
- --label (-l) N: column index for label (1-based)
- --icon (-i) N: column index for icon (1-based)
- --value (-V) N: column index for value (1-based)
- --active (-a) N: visually active item (1-based)
- --preselect (-P) N: preselected item (1-based)
- --stream (-s): stream stdin progressively

### Example

```bash
echo -e "Firefox\nAlacritty\nThunar" | walker --dmenu
```

With columns and a separator:

```bash
echo -e "Firefox;org.mozilla.firefox\nAlacritty;org.alacritty.Alacritty" \
  | walker --dmenu -t ";" -l 1 -i 2
```

## Service mode

Run as a background service for fast reopen:

```bash
walker --gapplication-service &
walker      # opens window via socket
```

## Autostart

Enable on login:

```bash
walker --enableautostart
```

Disable:

```bash
walker --disableautostart
```
