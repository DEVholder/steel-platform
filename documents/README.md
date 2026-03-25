# Steel Platform Docs

This directory is the canonical project brief for AI coding agents.

Start with the top-level development docs:

1. [30-prd.md](/Users/soo/workspace/steel-platform/documents/30-prd.md)
2. [31-requirements-spec.md](/Users/soo/workspace/steel-platform/documents/31-requirements-spec.md)
3. [32-use-cases.md](/Users/soo/workspace/steel-platform/documents/32-use-cases.md)
4. [33-data-model-erd.md](/Users/soo/workspace/steel-platform/documents/33-data-model-erd.md)
5. [34-implementation-brief.md](/Users/soo/workspace/steel-platform/documents/34-implementation-brief.md)

Then read only the base docs needed for your task.

Base docs:

- Overview: [01-overview.md](/Users/soo/workspace/steel-platform/documents/01-overview.md)
- System flow: [02-system-flow.md](/Users/soo/workspace/steel-platform/documents/02-system-flow.md)

Role-based reading:

- Building services: [03-services.md](/Users/soo/workspace/steel-platform/documents/03-services.md)
- Building normalization: [04-normalizer.md](/Users/soo/workspace/steel-platform/documents/04-normalizer.md)
- Implementing APIs: [05-api.md](/Users/soo/workspace/steel-platform/documents/05-api.md)
- Implementing persistence: [06-data-model.md](/Users/soo/workspace/steel-platform/documents/06-data-model.md)
- Planning delivery: [07-build-plan.md](/Users/soo/workspace/steel-platform/documents/07-build-plan.md)
- Operating the system: [08-operations.md](/Users/soo/workspace/steel-platform/documents/08-operations.md)

Current implementation details:

- Dev stack topology: [09-dev-topology.md](/Users/soo/workspace/steel-platform/documents/09-dev-topology.md)
- MCP to normalizer flow: [10-mcp-normalizer-integration.md](/Users/soo/workspace/steel-platform/documents/10-mcp-normalizer-integration.md)
- Normalizer I/O shape: [11-normalizer-contract.md](/Users/soo/workspace/steel-platform/documents/11-normalizer-contract.md)
- Raw artifact policy: [12-artifact-policy.md](/Users/soo/workspace/steel-platform/documents/12-artifact-policy.md)
- Session rules: [13-session-lifecycle.md](/Users/soo/workspace/steel-platform/documents/13-session-lifecycle.md)
- Local dev config: [14-local-dev-config.md](/Users/soo/workspace/steel-platform/documents/14-local-dev-config.md)
- Error and retry rules: [15-error-retry-policy.md](/Users/soo/workspace/steel-platform/documents/15-error-retry-policy.md)
- MVP verification: [16-mvp-test-plan.md](/Users/soo/workspace/steel-platform/documents/16-mvp-test-plan.md)
- Security and access rules: [17-security-access.md](/Users/soo/workspace/steel-platform/documents/17-security-access.md)
- Production topology: [18-production-topology.md](/Users/soo/workspace/steel-platform/documents/18-production-topology.md)
- Pending decisions: [19-open-decisions.md](/Users/soo/workspace/steel-platform/documents/19-open-decisions.md)
- Artifact access contract: [20-artifact-access-contract.md](/Users/soo/workspace/steel-platform/documents/20-artifact-access-contract.md)
- Anti-abuse access policy: [21-anti-abuse-access-policy.md](/Users/soo/workspace/steel-platform/documents/21-anti-abuse-access-policy.md)
- WARP egress strategy: [22-warp-egress-strategy.md](/Users/soo/workspace/steel-platform/documents/22-warp-egress-strategy.md)
- Compose service map: [23-compose-service-map.md](/Users/soo/workspace/steel-platform/documents/23-compose-service-map.md)
- Actionable view schema: [25-actionable-view-schema.md](/Users/soo/workspace/steel-platform/documents/25-actionable-view-schema.md)
- MCP tool contracts: [26-mcp-tool-contracts.md](/Users/soo/workspace/steel-platform/documents/26-mcp-tool-contracts.md)
- WARP compose pattern: [27-warp-compose-pattern.md](/Users/soo/workspace/steel-platform/documents/27-warp-compose-pattern.md)

Global rules:

- Steel Browser is the browser truth.
- The agent is the decision maker.
- The normalizer is an optimization layer, not a control layer.
- Extract-like results separate `semantic_summary` from `actionable_view`.
- Raw artifacts stay available by reference, not as the default response payload.
