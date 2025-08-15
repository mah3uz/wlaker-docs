---
title: Dmenu
nextjs:
  metadata:
    title: Dmenu
    description: Use Walker in dmenu-compatible mode, reading entries from stdin with column support.
---

Walker can emulate dmenu for broader script compatibility. See the CLI page for flags.

## Run

```bash
echo -e "one\ntwo\nthree" | walker --dmenu
```

Use label/icon/value columns and separators for richer entries.
