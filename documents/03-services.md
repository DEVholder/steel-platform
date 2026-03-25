# Steel Platform Services

## Core Services

### `steel-browser`

- executes browser actions
- holds live page and session state
- exposes raw artifacts

### `steel-mcp-server`

- exposes the agent-facing MCP entry point
- calls `steel-browser`
- routes extract flows through `content-normalizer`
- returns normalized output for extract-like operations

### `warp` sidecar

- provides an experimental egress layer for `steel-browser`
- should affect browser outbound traffic only
- should not own agent logic or normalization logic
- is currently a development-stage network isolation candidate, not a final production standard

### `content-normalizer`

- removes HTML noise
- preserves action-relevant structure
- returns compact outputs
- uses `ReaderLM-v2` as the default HTML-to-Markdown/JSON model in the MVP
- should be implemented behind a model-adapter boundary so other models can be added later

### `session-store`

- persists cookies and session metadata
- supports reuse by `session_id`

### `local-slm-adapter` (optional)

- improves semantic compression or classification
- never becomes the source of action truth

Read next:

- normalizer details: [04-normalizer.md](/Users/soo/workspace/steel-platform/documents/04-normalizer.md)
- API contracts: [05-api.md](/Users/soo/workspace/steel-platform/documents/05-api.md)
- persistence model: [06-data-model.md](/Users/soo/workspace/steel-platform/documents/06-data-model.md)
- dev stack layout: [09-dev-topology.md](/Users/soo/workspace/steel-platform/documents/09-dev-topology.md)
