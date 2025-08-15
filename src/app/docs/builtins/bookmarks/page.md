---
title: Bookmarks
nextjs:
  metadata:
    title: Bookmarks
    description: Save URLs with keywords and groups; open them quickly from Walker.
---

Quickly open URLs with optional keywords and groups.

## Configure

```toml
[builtins.bookmarks]
name = "bookmarks"
icon = "bookmark"
switcher_only = true

[[builtins.bookmarks.entries]]
label = "Walker"
url = "https://github.com/abenz1267/walker"
keywords = ["walker", "github"]

# Groups with prefixes
[[builtins.bookmarks.groups]]
label = "Docs"
prefix = "d:"
ignore_unprefixed = false
[[builtins.bookmarks.groups.entries]]
label = "Go"
url = "https://go.dev"
keywords = ["golang"]
```

Type keywords or use group prefixes, e.g., `d:go`.
