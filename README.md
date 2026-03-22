# Steel Platform

Steel Platform is a Steel-based browser automation platform for AI agents.

It is designed to go beyond a simple Playwright replacement by combining:

- Steel Browser as the browser execution runtime
- an agent-facing control layer such as Steel MCP or a custom gateway
- a content normalizer that reduces noisy HTML before large-model reasoning
- session persistence for multi-step workflows
- optional local SLM preprocessing for low-cost classification and compression

## Goals

- improve browser automation reliability on difficult websites
- centralize browser execution on the home server
- make browser interactions easier for AI agents to use
- reduce token waste by normalizing browser results
- preserve action-relevant page structure for follow-up automation

## Core Flow

```text
User -> AI Agent -> Steel MCP / Control Layer -> Steel Browser -> Content Normalizer -> AI Agent
```

## Repository Structure

- `documents/`
  - software design, product, architecture, API, data, and operations documents

## Current Focus

The current repository focus is design and planning.

The document set defines:

- product scope
- architecture
- request flow
- requirements
- use cases
- data model
- API contracts
- implementation backlog
- operations guidance

## Documentation Entry Point

Start here:

- [documents/steel-platform-docs-index.md](documents/steel-platform-docs-index.md)

## Notes

- Steel Browser is the execution runtime
- content normalization is a separate concern
- local SLM usage is optional and should not become the source of action truth

