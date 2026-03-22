# Steel Platform Task Backlog

## Purpose

This is the prioritized engineering backlog for the project.

It is written so an AI coding agent can execute tasks in order.

## Priority 0: Foundation

### Task 0.1

Confirm `steel-browser` deployment and external access.

Definition of done:

- local `3000` responds
- local `9223` responds
- reverse-proxied external domain responds

### Task 0.2

Create repository skeleton for the platform.

Definition of done:

- monorepo layout exists
- service directories created
- docs folder copied or linked

## Priority 1: Content Normalizer MVP

### Task 1.1

Build a FastAPI service for normalization input and output.

### Task 1.2

Implement HTML cleanup pipeline.

Must handle:

- script removal
- style removal
- boilerplate removal
- visible text extraction

### Task 1.3

Implement actionable structure extraction.

Must return:

- links
- buttons
- inputs
- forms

### Task 1.4

Implement semantic summary generation without local SLM.

Definition of done:

- JSON output includes `semantic_summary`
- JSON output includes `actionable_view`
- output size is measurably reduced compared with raw HTML

## Priority 2: Control Gateway MVP

### Task 2.1

Create control-gateway FastAPI service.

### Task 2.2

Implement browser client integration.

### Task 2.3

Implement:

- open
- click
- type
- wait
- extract
- screenshot

### Task 2.4

Make `extract` call the normalizer by default.

Definition of done:

- browser actions work against a live website
- normalized output is returned through the gateway

## Priority 3: Session Persistence

### Task 3.1

Create session data model.

### Task 3.2

Persist session metadata and cookies.

### Task 3.3

Allow requests to reuse prior sessions.

Definition of done:

- session ID can be reused across multiple actions
- auth state survives between requests where possible

## Priority 4: Optional Local SLM

### Task 4.1

Define local SLM adapter contract.

### Task 4.2

Implement optional summarization/classification call path.

### Task 4.3

Guard against action pollution by limiting SLM output to semantic layers.

Definition of done:

- local SLM is optional
- actionable structured view remains rule-based

## Priority 5: Production Hardening

### Task 5.1

Add logging and request IDs.

### Task 5.2

Add metrics for normalization reduction.

### Task 5.3

Add authentication and rate limiting to public APIs.

### Task 5.4

Add screenshots and raw HTML references for debugging.

## Suggested Agent Execution Order

1. repository skeleton
2. content normalizer
3. control gateway
4. browser integration
5. session persistence
6. optional local SLM
7. production hardening

