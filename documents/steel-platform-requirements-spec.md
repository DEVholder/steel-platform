# Steel Platform Requirements Specification

## 1. Purpose

This document defines the requirements for the Steel platform.

## 2. Functional Requirements

### FR-1 Browser Runtime

The system shall provide a browser runtime through Steel Browser.

### FR-2 Remote Access

The system shall allow authenticated remote access to the browser service through reverse proxy infrastructure.

### FR-3 Agent Control Interface

The system shall provide a control interface that an AI agent can use to request browser actions.

### FR-4 Session Creation

The system shall allow creation of reusable browser sessions.

### FR-5 Session Reuse

The system shall allow subsequent requests to reference and reuse prior sessions.

### FR-6 Browser Actions

The system shall support at least:

- open page
- click
- type
- wait
- extract
- screenshot

### FR-7 Normalization

The system shall transform raw browser output into normalized output.

### FR-8 Semantic Summary

The normalized output shall include a semantic summary suitable for AI reasoning.

### FR-9 Actionable View

The normalized output shall include an actionable structured view suitable for browser follow-up actions.

### FR-10 Artifact References

The system shall preserve references to raw browser artifacts for debugging and fallback.

### FR-11 Noise Reduction

The normalizer shall remove low-value noise such as scripts, styles, tracking markup, and repeated boilerplate when safe.

### FR-12 Action Preservation

The normalizer shall preserve action-relevant structures such as links, buttons, inputs, forms, and identifiers where possible.

### FR-13 Optional Local SLM

The system may optionally use a local SLM for semantic compression or classification.

### FR-14 SLM Isolation

The system shall not allow the local SLM to become the sole source of action truth.

## 3. Non-Functional Requirements

### NFR-1 Reliability

The platform should support multi-step browser workflows without requiring a new browser instance for every action.

### NFR-2 Security

Public entry points shall require authentication.

### NFR-3 Debug Isolation

Debug interfaces such as DevTools shall not be exposed publicly by default.

### NFR-4 Observability

The platform shall emit logs and identifiers sufficient to trace a request across services.

### NFR-5 Token Efficiency

The platform should substantially reduce browser output size before passing it to larger models.

### NFR-6 Modularity

The platform should be implementable as separable services so AI coding agents can work on components independently.

## 4. Constraints

- deployment target is a 16GB home server
- reverse proxy is already managed via Nginx Proxy Manager
- Docker-based deployment is preferred
- Steel Browser remains the browser execution engine

## 5. Acceptance Criteria

The first production-worthy milestone is accepted when:

1. the agent can open and interact with a real site through the control layer
2. extraction returns normalized output instead of raw HTML by default
3. the output supports a next action without requiring full page source inspection
4. session state can persist across multiple related requests

