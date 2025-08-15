---
title: Translation
nextjs:
  metadata:
    title: Translation
    description: Translate text via Google (free) or DeepL Free; supports direction hints in the query.
---

Translate text using Google (free) or DeepL (free API).

Providers:

- googlefree (no key needed)
- deeplfree (requires `DEEPL_AUTH_KEY`)

## Configure

```toml
[builtins.translation]
name = "translation"
icon = "accessories-dictionary"
placeholder = "Translation"
switcher_only = true
provider = "googlefree"
```

Query forms:

- `text>de` translate to German
- `en>text` translate from English
- `en>text>de` translate English to German

Enter copies the translated text to the clipboard.
