# MVP Test and Verification Plan

The first implementation should prove that the full browsing loop works.

Core verification targets:

- Steel Browser is reachable
- MCP can issue browser actions
- `extract` passes through the normalizer
- normalized output contains both `semantic_summary` and `actionable_view`
- session reuse works for a follow-up action

Minimum test layers:

- unit tests for normalizer behavior
- contract tests for API payload shapes
- local integration tests across the Compose stack
- one real-site smoke test for multi-step browsing

First milestone should be accepted only when:

1. an agent can open a real page
2. extract returns normalized output by default
3. the result is usable for a next step
4. session reuse works
5. failures are traceable through logs and artifact references

Current gate:

- documentation should be reviewed and accepted before current implementation is promoted as the repository baseline

Read next:

- build checkpoints: [07-build-plan.md](/Users/soo/workspace/steel-platform/documents/07-build-plan.md)
- operations baseline: [08-operations.md](/Users/soo/workspace/steel-platform/documents/08-operations.md)
