# Steel Platform Architecture Decision Records

## ADR-001: Use Steel Browser as the Browser Runtime

### Status

Accepted

### Context

Plain Playwright workflows have shown reliability issues on difficult sites.

### Decision

Use Steel Browser as the platform's browser execution runtime.

### Consequences

- improved browser execution strategy
- external dependency on Steel Browser API
- clearer separation between browser runtime and higher-level orchestration

## ADR-002: Separate Content Normalization from Browser Execution

### Status

Accepted

### Context

Raw browser output is too noisy for efficient AI-agent reasoning.

### Decision

Build Content Normalizer as a separate layer rather than assuming Steel Browser itself solves this problem.

### Consequences

- better token optimization
- clearer modularity
- additional service to maintain

## ADR-003: Preserve Dual Representations

### Status

Accepted

### Context

Aggressive summarization can corrupt the data needed for subsequent actions.

### Decision

Every normalized page should separate:

- semantic summary
- actionable structured view

### Consequences

- safer downstream actions
- slightly larger result payload than summary-only output
- more reliable agent planning

## ADR-004: Keep Local SLM Optional

### Status

Accepted

### Context

The project can gain value from local preprocessing, but must not depend on local SLM quality for correctness.

### Decision

Treat local SLM as an optional enhancement layer for semantic compression and classification only.

### Consequences

- simpler MVP
- reduced implementation risk
- easier to harden the rule-based pipeline first

## ADR-005: Keep DevTools Private

### Status

Accepted

### Context

Debug ports provide deep browser control and should not be publicly exposed by default.

### Decision

Keep `9223` local-only and use SSH tunneling or internal access when debugging is required.

### Consequences

- safer operational posture
- slightly less convenient remote debugging

