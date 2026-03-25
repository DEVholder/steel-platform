# Steel Platform System Flow

Canonical path:

```text
User -> AI Agent -> Control Gateway / MCP -> Steel Browser -> Content Normalizer -> AI Agent
```

Control rules:

- the user starts the task
- the AI agent decides the next step
- Steel Browser is the source of truth for page state
- the normalizer prepares compact outputs for reasoning

Extract-like responses should contain:

- `page_meta`
- `semantic_summary`
- `actionable_view`
- `artifacts`

If summarized output conflicts with browser state, trust the browser.

Read next:

- service boundaries: [03-services.md](/Users/soo/workspace/steel-platform/documents/03-services.md)
- normalizer behavior: [04-normalizer.md](/Users/soo/workspace/steel-platform/documents/04-normalizer.md)
- API shape: [05-api.md](/Users/soo/workspace/steel-platform/documents/05-api.md)
