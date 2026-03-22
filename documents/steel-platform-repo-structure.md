# Steel Platform Repository Structure

## Purpose

This document proposes a repository layout that is easy for both humans and AI coding agents to work in.

## Recommended Monorepo Layout

```text
steel-platform/
  README.md
  docker-compose.yml
  .env.example
  docs/
    architecture/
    operations/
    specs/
  services/
    control-gateway/
      app/
      tests/
      Dockerfile
      pyproject.toml
    content-normalizer/
      app/
      tests/
      Dockerfile
      pyproject.toml
    session-store/
      migrations/
      app/
      tests/
    local-slm-adapter/
      app/
      tests/
  shared/
    schemas/
    clients/
    logging/
    utils/
  scripts/
    dev/
    deploy/
    test/
```

## Service Ownership

### services/control-gateway

Contains:

- FastAPI app
- session-aware action handlers
- Steel Browser client integration
- request/response envelopes

### services/content-normalizer

Contains:

- cleanup logic
- extraction logic
- semantic summary generation
- actionable view generation

### services/session-store

Contains:

- persistence models
- cookie/session read and write operations

### services/local-slm-adapter

Contains:

- optional local model invocation code
- prompt templates for compression/classification

### shared/schemas

Contains:

- Pydantic or JSON schema models for:
  - session payloads
  - action requests
  - normalized page output

## Recommended Tech Layout

### Python Services

For each Python service:

- `app/main.py`
- `app/api/`
- `app/core/`
- `app/models/`
- `app/services/`
- `tests/`

## Documentation Layout

Recommended:

```text
docs/
  specs/
    build-spec.md
    api-contracts.md
    normalizer-spec.md
  architecture/
    overview.md
    request-flow.md
  operations/
    runbook.md
    deployment.md
```

## Why This Layout Helps AI Agents

- clear component boundaries
- easier task decomposition
- low ambiguity about where code belongs
- simple handoff between services

