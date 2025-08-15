---
title: AI
nextjs:
  metadata:
    title: AI
    description: Integrate Anthropic Claude and Google Gemini via prompts; includes keys for session control.
---

Integrate Anthropic Claude and Google Gemini via prompts.

{% callout title="Required Env vars:" %}
- ANTHROPIC_API_KEY: required for Anthropic
- GEMINI_API_KEY: required for Gemini
{% /callout %}

## Configure

```toml
[builtins.ai]
name = "ai"
placeholder = "AI"
show_sub_when_single = true
switcher_only = true

[[builtins.ai.anthropic.prompts]]
label = "General Assistant"
model = "claude-3-7-sonnet-20250219"
temperature = 1
max_tokens = 1000
prompt = "You are a helpful general assistant. Keep answers short."

[[builtins.ai.gemini.prompts]]
label = "Code Helper"
model = "gemini-1.5-pro"
temperature = 0.7
max_tokens = 800
prompt = "Be concise and provide code examples."
```

## Keys in AI view

- Ctrl+X: clear session
- Ctrl+C: copy last response
- Ctrl+R: resume session
- Ctrl+E: run last response in terminal
