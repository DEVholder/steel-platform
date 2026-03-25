# Steel Platform Overview

Steel Platform is a browser automation platform for AI agents.

It exists to solve:

- unreliable browser execution on difficult sites
- brittle login and session reuse
- raw HTML outputs that are too noisy for efficient reasoning

The platform is not just a browser container and not just an MCP server.
It combines:

- Steel Browser as the execution runtime
- a control layer for agent-facing actions
- a content normalizer for compact outputs
- session persistence for multi-step workflows

MVP success means:

1. an agent can browse a real site through the control layer
2. extract returns normalized output by default
3. the result supports a next action
4. session reuse works across related steps

Read next:

- system flow: [02-system-flow.md](/Users/soo/workspace/steel-platform/documents/02-system-flow.md)
- service boundaries: [03-services.md](/Users/soo/workspace/steel-platform/documents/03-services.md)
- delivery order: [07-build-plan.md](/Users/soo/workspace/steel-platform/documents/07-build-plan.md)
