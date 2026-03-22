# Steel Platform Agent Handoff Guide

## Purpose

This document is intended for another AI coding agent that will build the project.

It should be read as a direct implementation brief.

## Project Summary

Build a Steel-based browser automation platform for AI agents.

The system is not just a browser container. It must provide:

- browser execution through Steel Browser
- an agent-facing control interface
- normalized page results that reduce token cost
- session persistence
- optional local SLM preprocessing

## The Most Important Rule

Do not pass raw HTML directly back to the agent by default.

Instead:

1. collect browser output
2. normalize it
3. return semantic summary plus actionable structured view

## The Second Most Important Rule

Do not let semantic summarization corrupt browser action truth.

This means:

- actionable view must be conservative
- semantic summary may be compressed
- browser remains source of truth

## Components to Build

### 1. content-normalizer

Build this first.

Requirements:

- FastAPI service
- HTML cleanup
- visible text extraction
- link/button/input/form extraction
- semantic summary output
- actionable structured view output

### 2. control-gateway

Build this second.

Requirements:

- FastAPI service
- browser action endpoints
- session-aware requests
- call normalizer after extraction

### 3. session-store

Build this third.

Requirements:

- session ID persistence
- cookie state persistence
- metadata lookup

### 4. local-slm-adapter

Build only after the rule-based normalizer works well.

Requirements:

- optional integration
- semantic-only enhancement

## Concrete First Milestone

Deliver a working path where:

1. a request opens a real page in Steel Browser
2. page content is extracted
3. the normalizer removes noise
4. the gateway returns compact JSON
5. the response is usable for a second browser action

## Reference Output Shape

Every extract-like result should aim for:

```json
{
  "page_meta": {},
  "semantic_summary": {},
  "actionable_view": {},
  "artifacts": {}
}
```

## Minimum Action Set

The first build must support:

- open
- click
- type
- wait
- extract
- screenshot

## Development Priority

1. build the normalizer
2. build the gateway
3. integrate Steel Browser
4. add persistence
5. add optional SLM support

## Quality Bar

The implementation is acceptable only if:

- token-heavy markup is substantially reduced
- action-relevant UI data is preserved
- the system can support multi-step browsing
- failures are debuggable

## Deliverables Expected From the Implementing Agent

- working service code
- Dockerfiles where needed
- `.env.example`
- local run instructions
- API route documentation
- test coverage for normalizer behavior

