---
title: Themes & Layouts
nextjs:
  metadata:
    title: Themes & Layouts
    description: Compose the UI with layout TOML, theme stacks, and CSS; includes windowed mode notes and examples.
---

Walker composes a UI layout (containers and widgets) with a theme (sizes, positions) and CSS for colors/typography.

- Default layouts: `layout.default.toml` (layer shell) or `layout_window.default.toml` (window)
- Theme file stack: `theme_base` + `theme`
- CSS file: `default.css` (prepends pywal colors if present)

## Selecting a theme

```toml
theme = "default"
# theme_base = ["my-base"]
```

Additional lookup directories:

```toml
theme_location = ["~/dotfiles/walker/themes"]
```

## Theme structure

A theme TOML mirrors the UI structure. For example, to make the window 400px wide and the list max height 500px:

```toml
[ui.window]
width = -1
height = -1

[ui.window.box]
width = 400

[ui.window.box.scroll.list]
max_height = 500
```

Every node supports common fields like `width`, `height`, `opacity`, `h_align`, `v_align`, and `margins`.

## CSS

User CSS is written to `~/.config/walker/themes/default.css`. Walker prepends pywal’s `colors-waybar.css` if found.

### Example: accent color

```css
/* ~/.config/walker/themes/default.css */
.list .item.is-active { background: var(--color6); }
```

## Windowed mode

If Layer Shell isn’t available, Walker uses the window layout/theme variants automatically. You can force it via `as_window = true`.

