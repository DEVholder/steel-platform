# WARP Compose Pattern

The current preferred development pattern is:

- a dedicated `warp` sidecar container
- `steel-browser` attached to the `warp` network namespace
- `steel-mcp-server` and `content-normalizer` kept outside that namespace

## Preferred mode

- shared network namespace for `steel-browser`
- tunnel-oriented traffic handling instead of application proxy mode

## Why this is preferred

- browser traffic is broader than simple HTTP client requests
- proxy mode adds app compatibility constraints
- proxy mode may introduce timeout and protocol limitations
- shared namespace keeps the browser egress path closer to a full-device network path

## Non-goals

- do not place the full stack behind WARP
- do not make MCP dependent on WARP-specific logic
- do not let WARP change the normalizer contract

## Open engineering checks

- confirm container startup and health behavior when `steel-browser` shares the `warp` namespace
- confirm that browser sessions remain stable
- confirm that only browser egress is affected

Read next:

- WARP strategy: [22-warp-egress-strategy.md](/Users/soo/workspace/steel-platform/documents/22-warp-egress-strategy.md)
- compose service map: [23-compose-service-map.md](/Users/soo/workspace/steel-platform/documents/23-compose-service-map.md)
