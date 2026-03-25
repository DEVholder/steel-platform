# Artifact Access Contract

Artifacts are for verification and debugging, not for the default browsing loop.

Default rule:

- `extract` returns artifact references only

Supported references may include:

- `raw_html_ref`
- `screenshot_ref`
- optional trace references

Verification flow:

1. the agent receives normalized output
2. the agent decides whether verification is needed
3. the agent requests a specific artifact by reference
4. MCP returns only the requested artifact payload or location

Contract rules:

- artifact retrieval is explicit and separate from normal browsing actions
- the agent should request the smallest artifact needed for verification
- artifact access should be logged with `request_id` and `session_id`

Read next:

- artifact policy: [12-artifact-policy.md](/Users/soo/workspace/steel-platform/documents/12-artifact-policy.md)
- error handling: [15-error-retry-policy.md](/Users/soo/workspace/steel-platform/documents/15-error-retry-policy.md)
