# Implementation Brief

## Current MVP Build Order

1. Stand up the four-container dev stack.
2. Confirm official Steel MCP actions work against `steel-browser`.
3. Implement `extract_page`.
4. Implement `content-normalizer` with `ReaderLM-v2`.
5. Preserve official MCP labels into `actionable_view`.
6. Implement `get_artifact`.
7. Run the three PoCs before broad implementation.

## Current Reality Check

The current repository contains early implementation work, but it should not yet be treated as architecture truth.

Before more feature work lands on top of it, documentation remains the source of truth for:

- container boundaries
- MCP tool surface
- normalizer behavior
- artifact access rules

Implementation should be revalidated against these docs before additional expansion.

## Required PoCs

### PoC 1

`extract_page + official label preservation`

### PoC 2

`ReaderLM-v2 clean_html -> semantic_summary/actionable_view`

### PoC 3

`steel-browser + warp sidecar network behavior`

## Implementation Rules

- Prefer official Steel MCP tools before custom replacements.
- Keep custom additions minimal: `extract_page`, `get_artifact`.
- Use `clean_html` for model inference and keep `raw_html` as fallback.
- Treat labels as stale after page-changing actions.

## Immediate References

- [23-compose-service-map.md](/Users/soo/workspace/steel-platform/documents/23-compose-service-map.md)
- [26-mcp-tool-contracts.md](/Users/soo/workspace/steel-platform/documents/26-mcp-tool-contracts.md)
- [27-warp-compose-pattern.md](/Users/soo/workspace/steel-platform/documents/27-warp-compose-pattern.md)
