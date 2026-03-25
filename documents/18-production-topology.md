# Production Deployment Topology

This document describes the intended production shape.

Production is separate from local development.

## Intended Runtime

- home server deployment
- Docker-managed services
- reverse proxy in front of public endpoints

## Expected Components

- reverse proxy
- `steel-browser`
- `steel-mcp-server` or future gateway entry point
- `content-normalizer`
- optional session persistence store
- optional local SLM support

## Expected Topology

```text
AI Agent -> reverse proxy -> MCP / gateway -> steel-browser
                                      -> content-normalizer
                                      -> session-store
```

Rules:

- reverse proxy is production-only
- public entry points require authentication
- browser debug interfaces stay private
- internal services communicate on the private server network

This document is intentionally high level until production configuration is finalized.

Read next:

- security rules: [17-security-access.md](/Users/soo/workspace/steel-platform/documents/17-security-access.md)
- operations baseline: [08-operations.md](/Users/soo/workspace/steel-platform/documents/08-operations.md)
