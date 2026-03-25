# Compose Service Map

The current development stack uses four containers.

Services:

1. `steel-browser`
2. `steel-mcp-server`
3. `warp`
4. `content-normalizer`

Responsibility map:

- `steel-mcp-server`: agent entry point
- `steel-browser`: browser runtime
- `warp`: browser egress isolation candidate
- `content-normalizer`: HTML interpretation and compact output generation

Expected service relationships:

- `steel-mcp-server` calls `steel-browser`
- `steel-mcp-server` calls `content-normalizer`
- `steel-browser` routes outbound site traffic through `warp`

Non-goals:

- `warp` should not receive agent traffic directly
- `content-normalizer` should not depend on `warp`
- `steel-mcp-server` should not depend on model-specific internals

Read next:

- dev topology: [09-dev-topology.md](/Users/soo/workspace/steel-platform/documents/09-dev-topology.md)
- MCP integration: [10-mcp-normalizer-integration.md](/Users/soo/workspace/steel-platform/documents/10-mcp-normalizer-integration.md)
