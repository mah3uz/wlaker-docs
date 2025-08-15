---
title: Websearch
nextjs:
  metadata:
    title: Websearch
    description: Configure search engines and fire up web searches using %TERM% in URLs.
---

Fire up web searches using configured engines; can be switcher-only entries too.

## Configure

```toml
[builtins.websearch]
name = "websearch"
icon = "applications-internet"
placeholder = "Websearch"
keep_selection = true

  [[builtins.websearch.entries]]
  name = "Google"
  url = "https://www.google.com/search?q=%TERM%"

  [[builtins.websearch.entries]]
  name = "DuckDuckGo"
  url = "https://duckduckgo.com/?q=%TERM%"
  switcher_only = true

  [[builtins.websearch.entries]]
  name = "Ecosia"
  url = "https://www.ecosia.org/search?q=%TERM%"
  switcher_only = true
```

Use `%TERM%` placeholder to inject the current query.
