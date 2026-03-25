# Local Development Configuration Spec

Local development uses Docker Compose-managed containers.

Core local services:

- `steel-browser`
- `steel-mcp-server`
- `warp`
- `content-normalizer`

Local configuration should define:

- container names
- internal service hostnames
- exposed local ports
- shared network name
- environment variables for inter-service URLs

Minimum configuration areas:

- MCP URL for Steel Browser
- MCP URL for Content Normalizer
- browser API port
- warp proxy endpoint or sidecar connectivity settings
- WARP tunnel-only configuration if shared namespace mode is used
- normalizer API port
- `ReaderLM-v2` model configuration for the normalizer
- future model selection settings if additional backends are introduced

Rules:

- local configuration should assume no reverse proxy
- services should communicate through Compose networking
- production-specific routing config should stay out of the dev config
- model-specific settings should stay inside the normalizer configuration boundary
- warp-specific settings should stay isolated to the browser egress boundary

Read next:

- dev topology: [09-dev-topology.md](/Users/soo/workspace/steel-platform/documents/09-dev-topology.md)
- build order: [07-build-plan.md](/Users/soo/workspace/steel-platform/documents/07-build-plan.md)
