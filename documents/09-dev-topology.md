# Development Deployment Topology

Current development and test work assumes a local Docker Compose stack.

This stage does not use a reverse proxy.

Containers:

- `steel-browser`
- `steel-mcp-server`
- `warp`
- `content-normalizer`

Current intent:

- `steel-browser` runs the live browser runtime
- `steel-mcp-server` is the agent-facing entry point
- `warp` is an experimental egress sidecar for browser outbound traffic only
- `content-normalizer` receives browser output and returns compact results
- `content-normalizer` uses `ReaderLM-v2` as the default local model during MVP development

Topology:

```text
AI Agent -> steel-mcp-server -> steel-browser -> warp -> Target Site
                           \-> content-normalizer
```

Rules:

- local development uses container-to-container networking
- the agent should talk to MCP, not directly to the browser
- `warp` should be scoped to browser egress only
- reverse proxy and public exposure are deferred to production planning

Read next:

- integration flow: [10-mcp-normalizer-integration.md](/Users/soo/workspace/steel-platform/documents/10-mcp-normalizer-integration.md)
- local config: [14-local-dev-config.md](/Users/soo/workspace/steel-platform/documents/14-local-dev-config.md)
- warp candidate design: [22-warp-egress-strategy.md](/Users/soo/workspace/steel-platform/documents/22-warp-egress-strategy.md)
