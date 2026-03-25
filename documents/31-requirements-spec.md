# Requirements Specification

## Functional Requirements

### FR-1 Browser Runtime

The system shall provide browser execution through `steel-browser`.

### FR-2 Agent Entry Point

The system shall expose browser control to the agent through `steel-mcp-server`.

### FR-3 Core Browser Actions

The system shall support the official Steel MCP tool set used by the project, including navigation, click, type, wait, and screenshot flows.

### FR-4 Normalized Extraction

The system shall provide `extract_page` that routes current page data through `content-normalizer`.

### FR-5 Label Preservation

When official MCP labels are available, the system shall preserve them in `actionable_view`.

### FR-6 Artifact Fallback

The system shall return artifact references by default and support explicit artifact retrieval.

### FR-7 Session Reuse

The system shall support reusable browser sessions for multi-step workflows.

### FR-8 Model Backend

The MVP normalizer shall use `ReaderLM-v2` behind a model-adapter boundary.

## Non-Functional Requirements

### NFR-1 Token Efficiency

The system should reduce token-heavy browser output before agent reasoning.

### NFR-2 Action Safety

The normalizer must not create a competing action label namespace.

### NFR-3 Modularity

Steel Browser, MCP, normalizer, and artifact access should remain separable components.

### NFR-4 Observability

The system should log request, session, action, and artifact-access context.

### NFR-5 Controlled Verification

Raw artifacts should be retrieved only through explicit follow-up actions.

### NFR-6 Network Isolation

If `warp` is used, it should affect browser egress only.

Reference docs:

- [11-normalizer-contract.md](/Users/soo/workspace/steel-platform/documents/11-normalizer-contract.md)
- [20-artifact-access-contract.md](/Users/soo/workspace/steel-platform/documents/20-artifact-access-contract.md)
- [25-actionable-view-schema.md](/Users/soo/workspace/steel-platform/documents/25-actionable-view-schema.md)
- [26-mcp-tool-contracts.md](/Users/soo/workspace/steel-platform/documents/26-mcp-tool-contracts.md)
