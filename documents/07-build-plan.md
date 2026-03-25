# Build Plan

Recommended build order:

1. confirm `steel-browser` deployment and access
2. build `content-normalizer`
3. build `control-gateway`
4. integrate browser actions end to end
5. add `session-store`
6. add optional `local-slm-adapter`
7. add production hardening

MVP action set:

- `open`
- `click`
- `type`
- `wait`
- `extract`
- `screenshot`

First milestone is complete when:

1. an agent can browse a real site
2. extract returns normalized output
3. the result supports a follow-up action
4. session reuse works
5. failures are inspectable

Read next:

- operations and health checks: [08-operations.md](/Users/soo/workspace/steel-platform/documents/08-operations.md)
- service boundaries: [03-services.md](/Users/soo/workspace/steel-platform/documents/03-services.md)
