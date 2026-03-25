# API Contracts

## Control Gateway

Base path:

- `/api/v1`

Endpoints:

- `POST /sessions`
- `GET /sessions/{session_id}`
- `POST /actions/open`
- `POST /actions/click`
- `POST /actions/type`
- `POST /actions/wait`
- `POST /actions/extract`
- `POST /actions/screenshot`

## Content Normalizer

Base path:

- `/normalize/v1`

Endpoints:

- `POST /page`
- `POST /html`

## Shared Response Envelope

```json
{
  "ok": true,
  "request_id": "req_123",
  "session_id": "sess_123",
  "result": {},
  "error": null
}
```

## Core Rules

- action endpoints accept `session_id`
- extract normalizes by default
- raw HTML is not returned by default
- every response carries `request_id`

Read next:

- data entities: [06-data-model.md](/Users/soo/workspace/steel-platform/documents/06-data-model.md)
- build order: [07-build-plan.md](/Users/soo/workspace/steel-platform/documents/07-build-plan.md)
