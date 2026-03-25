# Raw Artifact and Fallback Policy

Artifacts exist to preserve a fallback path when normalized output is not enough.

Artifacts may include:

- raw HTML
- screenshots
- optional traces
- optional browser debug references

Rules:

- raw HTML should not be returned to the agent by default
- screenshots should not be the primary reasoning payload
- artifacts should be referenced, not embedded
- when normalized output is uncertain, the system should fall back to browser truth and artifact inspection
- artifact access should be explicit and separate from the default extract response

Typical flow:

1. agent receives normalized output
2. agent uses `actionable_view` if it is sufficient
3. if the result is ambiguous, inspect artifact references
4. if there is still conflict, defer to the live browser state

Label safety rule:

- if there is doubt about whether an actionable element still matches the live page, the agent should re-run extract and use the fresh MCP labels rather than trust stale mappings

This policy protects token budget while preserving debuggability.

Read next:

- MCP integration: [10-mcp-normalizer-integration.md](/Users/soo/workspace/steel-platform/documents/10-mcp-normalizer-integration.md)
- operations: [08-operations.md](/Users/soo/workspace/steel-platform/documents/08-operations.md)
