# WARP Egress Strategy

This document describes the current development-stage plan for isolating browser egress from the rest of the stack.

Current direction:

- use a dedicated `warp` container as a sidecar candidate
- scope it to `steel-browser` outbound traffic only
- keep `steel-mcp-server` and `content-normalizer` outside that egress path

Target shape:

```text
AI Agent -> steel-mcp-server -> steel-browser -> warp -> Target Site
                           \-> content-normalizer
```

Design intent:

- reduce the blast radius of browser outbound networking decisions
- avoid coupling the entire development stack to the same network policy
- keep browser egress replaceable later

Rules:

- MCP should not depend on WARP-specific behavior
- the normalizer contract must remain unchanged whether WARP is present or not
- WARP is currently a candidate egress layer, not a permanent product requirement

Open engineering questions:

- whether `steel-browser` should route through WARP by shared network namespace or proxy mode
- how session stability behaves when the browser egress path changes
- whether WARP is suitable beyond development experiments

Read next:

- dev topology: [09-dev-topology.md](/Users/soo/workspace/steel-platform/documents/09-dev-topology.md)
- local config: [14-local-dev-config.md](/Users/soo/workspace/steel-platform/documents/14-local-dev-config.md)
