# Product Requirements Document

## Product

Steel Platform is a browser automation platform for AI agents.

## Problem

The current browser automation path is too fragile for real-world AI-driven workflows because:

- difficult sites break plain automation more often than desired
- login and session reuse are brittle
- raw HTML is too large and noisy for efficient reasoning
- agents need a safer way to inspect pages and continue actions

## Product Goal

Build a Steel-based platform that lets an AI agent:

- control a real browser through MCP
- receive normalized page output instead of raw HTML by default
- continue multi-step browser workflows using preserved action labels
- fall back to artifacts only when verification is needed

## MVP Scope

- `steel-browser`
- `steel-mcp-server`
- `content-normalizer` with `ReaderLM-v2`
- artifact references and explicit artifact retrieval
- local Docker Compose dev stack
- optional `warp` egress sidecar as a development experiment

## Out of Scope for MVP

- production-grade multi-tenant user management
- broad anti-bot bypass functionality
- general-purpose RPA replacement
- final production egress strategy

## Success Criteria

1. An agent can browse a real site through MCP.
2. `extract_page` returns normalized output by default.
3. `actionable_view` preserves official MCP labels.
4. The agent can perform a follow-up action from normalized output.
5. Raw artifacts are available by reference for explicit verification.

## Key Product Rules

- Steel Browser is the browser truth.
- Official MCP labels are the action truth.
- The normalizer is an optimization layer, not a control layer.
- Raw HTML is preserved for fallback, not returned by default.

Base references:

- [01-overview.md](/Users/soo/workspace/steel-platform/documents/01-overview.md)
- [02-system-flow.md](/Users/soo/workspace/steel-platform/documents/02-system-flow.md)
- [10-mcp-normalizer-integration.md](/Users/soo/workspace/steel-platform/documents/10-mcp-normalizer-integration.md)
