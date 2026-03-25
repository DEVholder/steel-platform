# Normalizer Input and Output Contract

## Input

The MCP server should send the normalizer a compact browser-result payload.

Backend note:

- the MVP normalizer backend uses `ReaderLM-v2`
- the request and response contract must remain model-agnostic so other backends can be added later

Minimum input:

- `page_meta.url`
- `page_meta.title`
- `raw_html`
- `clean_html`
- `visible_text`
- `elements.links`
- `elements.buttons`
- `elements.inputs`
- `elements.forms`
- `elements.*.mcp_label` when available
- `artifacts.screenshot_ref`

Preferred shape:

```json
{
  "page_meta": {
    "url": "https://example.com",
    "title": "Example"
  },
  "raw_html": "<html>...</html>",
  "clean_html": "<main>...</main>",
  "visible_text": "Visible text here",
  "elements": {
    "links": [],
    "buttons": [],
    "inputs": [],
    "forms": []
  },
  "artifacts": {
    "screenshot_ref": "artifact://page/1/screenshot"
  }
}
```

## Output

The normalizer should return:

- `page_meta`
- `semantic_summary`
- `actionable_view`
- `artifacts`
- optional `metrics`

Preferred shape:

```json
{
  "page_meta": {},
  "semantic_summary": {},
  "actionable_view": {},
  "artifacts": {},
  "metrics": {}
}
```

Rules:

- `semantic_summary` is for reasoning
- `actionable_view` is for follow-up browser actions
- output should keep selector hints or stable ids where possible
- artifacts should be returned by reference, not inline
- backend model choice must not change the external schema
- raw artifacts should be lazily retrievable through references, not included in the default payload
- when official MCP labels are present in the input, the output should preserve them
- the normalizer must not create a competing action label namespace
- `raw_html` is preserved for fallback, while model inference should prefer `clean_html`

Read next:

- normalizer behavior: [04-normalizer.md](/Users/soo/workspace/steel-platform/documents/04-normalizer.md)
- artifact handling: [12-artifact-policy.md](/Users/soo/workspace/steel-platform/documents/12-artifact-policy.md)
