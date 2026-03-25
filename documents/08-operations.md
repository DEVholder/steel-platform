# Operations

Target environment:

- Ubuntu 24.04 home server
- Gemtek k12 mini PC
- 16 GB RAM
- Nginx Proxy Manager
- Docker and Portainer

Network rules:

- `3000` is the main Steel Browser API
- `9223` stays local-only for debug
- public entry points require authentication
- raw artifacts stay private

Health checks:

- Steel Browser responds
- reverse proxy routes correctly
- control-gateway can open a page
- normalizer produces reduced output

Logging baseline:

- `request_id`
- `session_id`
- target URL
- action type and status
- normalization reduction metrics
- screenshot reference on failure
- challenge or block-page detection events

Read next:

- delivery checkpoints: [07-build-plan.md](/Users/soo/workspace/steel-platform/documents/07-build-plan.md)
- persistence entities: [06-data-model.md](/Users/soo/workspace/steel-platform/documents/06-data-model.md)
- anti-abuse rules: [21-anti-abuse-access-policy.md](/Users/soo/workspace/steel-platform/documents/21-anti-abuse-access-policy.md)
