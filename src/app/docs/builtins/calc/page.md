---
title: Calc
nextjs:
  metadata:
    title: Calc
    description: Inline calculator with optional number requirement and minimum characters filtering.
---

Inline calculator. Requires number input when `require_number = true`.

## Configure

```toml
[builtins.calc]
name = "calc"
icon = "accessories-calculator"
placeholder = "Calculator"
min_chars = 4
require_number = true
```

Example: type `2+2` or `sqrt(9)` to get a result you can copy.
