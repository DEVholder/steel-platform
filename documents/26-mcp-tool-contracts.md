# MCP Tool Contracts

The project should use the official Steel MCP tools wherever possible.

Official tools currently expected:

- `navigate`
- `search`
- `click`
- `type`
- `scroll_down`
- `scroll_up`
- `go_back`
- `wait`
- `save_unmarked_screenshot`

Project-specific additions:

- `extract_page`
- `get_artifact`

## Label Preservation Rule

Official Steel MCP interactions use numbered labels for actionable elements.

These labels are the source of truth for action execution.

Rules:

- `click` and `type` should use official MCP labels
- `extract_page` should collect those labels and pass them into the normalizer input
- the normalizer should preserve `mcp_label` in `actionable_view` when available
- the normalizer must not create a competing label system
- after any page-changing action, prior labels should be treated as stale until a fresh extract is run

## Recommended `extract_page` behavior

`extract_page` should:

1. capture page state from the browser
2. collect official MCP-labeled interactive elements
3. send page content plus labeled elements to the normalizer
4. return normalized output with preserved `mcp_label` fields

## Recommended `get_artifact` behavior

`get_artifact` should:

- accept an artifact reference
- return only the requested artifact payload or location
- stay separate from normal browsing actions

Read next:

- normalizer contract: [11-normalizer-contract.md](/Users/soo/workspace/steel-platform/documents/11-normalizer-contract.md)
- artifact access: [20-artifact-access-contract.md](/Users/soo/workspace/steel-platform/documents/20-artifact-access-contract.md)
