# Security and Access Policy

This document defines the minimum security posture for the platform.

## Development Stage

Current assumptions:

- development runs on a local Docker Compose stack
- no reverse proxy is required for local development
- container-to-container traffic stays on the local Docker network

Development rules:

- the AI agent should talk to `steel-mcp-server`, not directly to `steel-browser`
- `steel-browser` debug access should stay internal to the local machine
- raw HTML and screenshots should not become the default response payload
- if `warp` is used, it should apply to browser egress only and not to the entire local stack

## Production Stage

Production assumptions:

- deployment will run on the home server
- reverse proxy will sit in front of the public entry points
- public exposure is limited to required endpoints only

Production minimums:

- require authentication on public APIs
- keep DevTools and internal browser debug endpoints private
- keep session storage and raw artifacts private
- preserve audit logs for browser actions

## Access Boundaries

### Public

- authenticated MCP or gateway entry point

### Private

- Steel Browser debug interfaces
- session persistence internals
- raw artifact storage
- optional local model internals

## Core Security Rules

- browser truth stays in the browser runtime
- normalized output is the default agent-facing payload
- artifact references are safer than inline raw payloads
- public exposure should be added only in production-specific config
- challenge or block responses should trigger a controlled stop or backoff path

Open decisions still needed:

- production authentication mechanism
- artifact access rules
- session ownership rules
- whether `warp` remains a dev-only experiment or becomes part of a longer-term deployment option

Read next:

- dev topology: [09-dev-topology.md](/Users/soo/workspace/steel-platform/documents/09-dev-topology.md)
- production topology: [18-production-topology.md](/Users/soo/workspace/steel-platform/documents/18-production-topology.md)
