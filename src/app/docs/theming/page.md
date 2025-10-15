---
title: Theming
nextjs:
  metadata:
    title: Theming
    description: Customize Walker's appearance with themes, CSS styling, and custom layouts.
---

Walker's appearance is fully customizable through themes. Themes consist of CSS styling and GTK4 XML layouts.

## Theme Structure

Themes are located in `~/.config/walker/themes/`. Each theme is a directory containing:

```text
~/.config/walker/themes/
└── your-theme/
    ├── style.css              # CSS styling
    ├── layout.xml             # Main window layout
    ├── item.xml               # Default item layout
    ├── item_calc.xml          # Calculator item layout
    ├── item_files.xml         # File browser item layout
    ├── item_clipboard.xml     # Clipboard item layout
    ├── item_symbols.xml       # Symbols item layout
    ├── item_todo.xml          # Todo item layout
    ├── item_providerlist.xml  # Provider list item layout
    ├── item_dmenu.xml         # Dmenu item layout
    ├── item_archlinuxpkgs.xml # Arch packages item layout
    ├── item_unicode.xml       # Unicode item layout
    ├── keybind.xml            # Keybind display layout
    └── preview.xml            # Preview pane layout
```

## Theme Inheritance

Themes inherit from the `default` theme automatically. You only need to include files you want to customize.

**Example:** To create a theme with custom colors but default layouts:

```text
~/.config/walker/themes/
└── my-theme/
    └── style.css    # Only this file - layouts inherited from default
```

**Important:** The default theme (`resources/themes/default/`) cannot be modified directly. Always create a custom theme.

## Creating a Theme

### 1. Create Theme Directory

```bash
mkdir -p ~/.config/walker/themes/my-theme
```

### 2. Create CSS File

Create `~/.config/walker/themes/my-theme/style.css`:

```css
/* Color definitions */
@define-color window_bg_color #1f1f28;
@define-color accent_bg_color #54546d;
@define-color theme_fg_color #f2ecbc;
@define-color error_bg_color #C34043;
@define-color error_fg_color #DCD7BA;

/* Reset all styles */
* {
  all: unset;
}

/* Window wrapper */
.box-wrapper {
  box-shadow:
    0 19px 38px rgba(0, 0, 0, 0.3),
    0 15px 12px rgba(0, 0, 0, 0.22);
  background: @window_bg_color;
  padding: 20px;
  border-radius: 20px;
  border: 1px solid darker(@accent_bg_color);
}

/* Input field */
.input {
  caret-color: @theme_fg_color;
  background: lighter(@window_bg_color);
  padding: 10px;
  color: @theme_fg_color;
  border-radius: 10px;
}

.input placeholder {
  opacity: 0.5;
}

/* List items */
.list {
  color: @theme_fg_color;
}

.item-box {
  border-radius: 10px;
  padding: 10px;
}

child:hover .item-box,
child:selected .item-box {
  background: alpha(@accent_bg_color, 0.25);
}

.item-text {
  font-size: 14px;
}

.item-subtext {
  font-size: 12px;
  opacity: 0.5;
}

.item-image,
.item-image-text {
  margin-right: 10px;
}

/* Quick activation labels */
.item-quick-activation {
  margin-left: 10px;
  background: alpha(@accent_bg_color, 0.25);
  border-radius: 5px;
  padding: 10px;
}

/* Placeholders */
.placeholder,
.elephant-hint {
  color: @theme_fg_color;
  opacity: 0.5;
}

/* Keybinds display */
.keybinds-wrapper {
  border-top: 1px solid lighter(@window_bg_color);
  font-size: 12px;
  opacity: 0.5;
  color: @theme_fg_color;
}

.keybind-bind {
  font-weight: bold;
  text-transform: lowercase;
}

/* Error display */
.error {
  padding: 10px;
  background: @error_bg_color;
  color: @error_fg_color;
  border-radius: 5px;
}

/* Preview pane */
.preview {
  border: 1px solid alpha(@accent_bg_color, 0.25);
  padding: 10px;
  border-radius: 10px;
  color: @theme_fg_color;
}

/* Icon sizes */
.normal-icons {
  -gtk-icon-size: 16px;
}

.large-icons {
  -gtk-icon-size: 32px;
}

/* Hide scrollbar */
scrollbar {
  opacity: 0;
}
```

### 3. Configure Walker to Use Theme

Edit `~/.config/walker/config.toml`:

```toml
theme = "my-theme"
```

### 4. Test Theme

```bash
walker
```

## CSS Styling Reference

### Main Components

| Class                  | Description                      |
|------------------------|----------------------------------|
| `.box-wrapper`         | Main window container            |
| `.box`                 | Content box                      |
| `.search-container`    | Input field container            |
| `.input`               | Search input field               |
| `.input placeholder`   | Input placeholder text           |
| `.content-container`   | Results container                |
| `.list`                | Results list                     |
| `.placeholder`         | Empty results placeholder        |
| `.elephant-hint`       | "Waiting for Elephant" message   |
| `.scroll`              | Scroll container                 |

### List Items

| Class                   | Description                      |
|-------------------------|----------------------------------|
| `.item-box`             | Item container                   |
| `.item-text-box`        | Text container                   |
| `.item-text`            | Main item text                   |
| `.item-subtext`         | Secondary item text              |
| `.item-image`           | Item icon                        |
| `.item-image-text`      | Text-based icon (emoji, etc.)    |
| `.item-quick-activation`| Quick activation label (F1, F2)  |

### States

| Selector              | Description                        |
|-----------------------|------------------------------------|
| `child:hover`         | Item hover state                   |
| `child:selected`      | Item selected state                |
| `.input:focus`        | Input field focused                |
| `.input:active`       | Input field active                 |

### Provider-Specific Classes

| Class                  | Description                      |
|------------------------|----------------------------------|
| `.calc`                | Calculator items                 |
| `.calc .item-text`     | Calculator result text           |
| `.symbols .item-image` | Symbol picker icons              |
| `.todo.done`           | Completed todo items             |
| `.todo.urgent`         | Urgent todo items                |
| `.todo.active`         | Active todo items                |
| `.bluetooth.disconnected` | Disconnected Bluetooth devices |

### Other Elements

| Class              | Description                          |
|--------------------|--------------------------------------|
| `.preview`         | Preview pane                         |
| `.keybinds-wrapper`| Keybindings display container        |
| `.keybinds`        | Keybindings list                     |
| `.keybind`         | Individual keybind                   |
| `.keybind-bind`    | Keybind key combination              |
| `.keybind-label`   | Keybind action label                 |
| `.error`           | Error message display                |

## Color System

### Standard Color Variables

```css
@define-color window_bg_color #1f1f28;     /* Window background */
@define-color accent_bg_color #54546d;     /* Accent color for highlights */
@define-color theme_fg_color #f2ecbc;      /* Text color */
@define-color error_bg_color #C34043;      /* Error background */
@define-color error_fg_color #DCD7BA;      /* Error text */
```

### Color Functions

GTK4 CSS supports color manipulation:

```css
/* Lighten color */
background: lighter(@window_bg_color);

/* Darken color */
border: 1px solid darker(@accent_bg_color);

/* Alpha transparency */
background: alpha(@accent_bg_color, 0.25);

/* Mix colors */
color: mix(@window_bg_color, @theme_fg_color, 0.5);
```

## Custom Layouts

You can customize the layout of Walker's UI using GTK4 XML.

### Main Layout (layout.xml)

The main window structure. Customize to change window size, spacing, orientation, etc.

**Example:** Create `~/.config/walker/themes/my-theme/layout.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<interface>
  <requires lib="gtk" version="4.0"></requires>
  <object class="GtkWindow" id="Window">
    <style>
      <class name="window"></class>
    </style>
    <property name="resizable">true</property>
    <property name="title">Walker</property>
    <child>
      <object class="GtkBox" id="BoxWrapper">
        <style>
          <class name="box-wrapper"></class>
        </style>
        <property name="orientation">horizontal</property>
        <property name="valign">center</property>
        <property name="halign">center</property>
        <property name="width-request">600</property>
        <property name="height-request">550</property>
        <!-- Content here -->
      </object>
    </child>
  </object>
</interface>
```

### Item Layouts

Customize how items appear in results.

**Example:** Custom calculator item layout `item_calc.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<interface>
  <template class="WalkerItem">
    <property name="hexpand">true</property>
    <style>
      <class name="item"></class>
      <class name="calc"></class>
    </style>
    <child>
      <object class="GtkBox" id="ItemBox">
        <style>
          <class name="item-box"></class>
        </style>
        <property name="orientation">horizontal</property>
        <property name="hexpand">true</property>
        <child>
          <object class="GtkImage" id="ItemImage">
            <style>
              <class name="item-image"></class>
              <class name="large-icons"></class>
            </style>
          </object>
        </child>
        <child>
          <object class="GtkBox" id="ItemTextBox">
            <style>
              <class name="item-text-box"></class>
            </style>
            <property name="orientation">vertical</property>
            <property name="hexpand">true</property>
            <child>
              <object class="GtkLabel" id="ItemText">
                <style>
                  <class name="item-text"></class>
                </style>
                <property name="xalign">0</property>
              </object>
            </child>
            <child>
              <object class="GtkLabel" id="ItemSubtext">
                <style>
                  <class name="item-subtext"></class>
                </style>
                <property name="xalign">0</property>
              </object>
            </child>
          </object>
        </child>
        <child>
          <object class="GtkLabel" id="ItemQuickActivation">
            <style>
              <class name="item-quick-activation"></class>
            </style>
          </object>
        </child>
      </object>
    </child>
  </template>
</interface>
```

## Example Themes

### Minimal Dark Theme

```css
@define-color window_bg_color #000000;
@define-color accent_bg_color #333333;
@define-color theme_fg_color #ffffff;

* {
  all: unset;
}

.box-wrapper {
  background: @window_bg_color;
  padding: 10px;
  border: 1px solid @accent_bg_color;
}

.input {
  background: @accent_bg_color;
  color: @theme_fg_color;
  padding: 8px;
}

.item-box {
  padding: 8px;
}

child:selected .item-box {
  background: @accent_bg_color;
}
```

### Colorful Theme

```css
@define-color window_bg_color #282c34;
@define-color accent_bg_color #61afef;
@define-color theme_fg_color #abb2bf;
@define-color error_bg_color #e06c75;
@define-color error_fg_color #282c34;
@define-color success_color #98c379;
@define-color warning_color #e5c07b;

* {
  all: unset;
}

.box-wrapper {
  background: @window_bg_color;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
}

.input {
  background: lighter(@window_bg_color);
  color: @theme_fg_color;
  padding: 12px;
  border-radius: 8px;
  border-left: 3px solid @accent_bg_color;
}

.item-box {
  padding: 10px;
  border-radius: 8px;
}

child:selected .item-box {
  background: @accent_bg_color;
  color: @window_bg_color;
}

.calc .item-text {
  color: @success_color;
}

.todo.urgent .item-text {
  color: @error_bg_color;
}
```

### Transparent/Blurred Theme

```css
@define-color window_bg_color rgba(0, 0, 0, 0.8);
@define-color accent_bg_color rgba(255, 255, 255, 0.1);
@define-color theme_fg_color #ffffff;

* {
  all: unset;
}

.box-wrapper {
  background: @window_bg_color;
  padding: 15px;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.input {
  background: @accent_bg_color;
  color: @theme_fg_color;
  padding: 10px;
  border-radius: 8px;
}

.item-box {
  padding: 10px;
  border-radius: 8px;
}

child:selected .item-box {
  background: rgba(255, 255, 255, 0.2);
}
```

## Tips and Best Practices

### 1. Use Color Variables

Define colors as variables for easy customization:

```css
@define-color my_color #ff0000;
background: @my_color;
```

### 2. Test Changes Live

Walker doesn't require restart for theme changes. Just reopen Walker to see updates.

### 3. Start Simple

Begin with just `style.css`, then add custom layouts if needed.

### 4. Inspect Default Theme

Check `~/.config/walker/themes/default/` (or `resources/themes/default/` in the repo) for reference.

### 5. Provider-Specific Styling

Use provider classes to style specific item types:

```css
.calc .item-text {
  font-family: monospace;
  font-size: 18px;
}

.files .item-image {
  -gtk-icon-size: 24px;
}
```

### 6. State-Based Styling

Style items based on their state:

```css
.todo.done {
  opacity: 0.5;
  text-decoration: line-through;
}

.bluetooth.disconnected {
  opacity: 0.3;
}
```

### 7. Responsive Sizing

Use relative units where appropriate:

```css
.item-text {
  font-size: 1em;
}

.item-subtext {
  font-size: 0.8em;
}
```

## GTK4 Resources

For detailed GTK4 widget documentation:
- [GTK4 Documentation](https://docs.gtk.org/gtk4/)
- [GTK4 CSS Properties](https://docs.gtk.org/gtk4/css-properties.html)
- [GTK4 Widget Gallery](https://docs.gtk.org/gtk4/visual_index.html)

## Nix Configuration

If using the Nix Home Manager module, define themes in your configuration:

```nix
programs.walker = {
  enable = true;
  config = {
    theme = "my-theme";
  };

  themes = {
    "my-theme" = {
      style = ''
        @define-color window_bg_color #1f1f28;
        /* More CSS here */
      '';

      layouts = {
        "layout" = ''<?xml version="1.0"?><!-- XML here -->'';
        "item_calc" = ''<?xml version="1.0"?><!-- XML here -->'';
      };
    };
  };
};
```

## Troubleshooting

### Theme Not Loading

1. Check theme name in config matches directory name
2. Ensure `style.css` exists in theme directory
3. Check for CSS syntax errors

### Styles Not Applying

1. Verify CSS selector syntax
2. Check for conflicting styles
3. Ensure classes match layout XML

### Layout Issues

1. Validate XML syntax
2. Check GTK4 widget property names
3. Ensure all required properties are set

## Next Steps

- [Configuration](/docs/configuration) - Configure Walker
- [Advanced Usage](/docs/advanced-usage) - Advanced customization
- View default theme: `resources/themes/default/` in [Walker GitHub repository](https://github.com/abenz1267/walker/tree/master/resources/themes/default)
