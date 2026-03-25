# Open Decisions

This document lists the few decisions that still need explicit user input.

Everything else can proceed from the current docs.

## Decision 1: Production Authentication

Needed for:

- reverse proxy configuration
- public API exposure
- artifact access rules

Options still open:

- proxy-only auth
- application bearer token auth
- both proxy auth and application auth

## Decision 2: Artifact Access Mode

Needed for:

- raw HTML fallback
- screenshot inspection
- debugging workflows

Options still open:

- internal-only references
- MCP-mediated retrieval only
- direct authenticated artifact API

## Decision 3: Session Scope

Needed for:

- session reuse safety
- multi-site browsing behavior
- cookie isolation

Options still open:

- one session per site
- one session per workflow
- mixed model with site scope metadata

## Decision 4: Local SLM Packaging

Current decision:

- MVP uses `ReaderLM-v2`
- model execution is owned by `content-normalizer`
- future models should be addable through an adapter-style backend boundary

Remaining detail:

- whether future alternative models run in the same container or as separate services

## Decision 5: MCP Output Shape

Needed for:

- implementation of the MCP wrapper
- agent integration expectations

Current default assumption:

- MCP returns normalized output for `extract`
- other actions return status-oriented payloads

This should be confirmed before implementation starts.

## Decision 6: WARP Usage Scope

Current default assumption:

- `warp` is a development-stage egress isolation experiment
- it should only affect `steel-browser` outbound traffic

Still open:

- whether the project will keep `warp` as an optional local dev component only
- whether a different egress strategy will replace it in production

Current technical preference:

- prefer shared network namespace with tunnel-only behavior over proxy mode for the browser runtime

## Decision 7: Implementation Reset Scope

Current concern:

- recent implementation work has diverged in quality from the intended architecture and needs re-review before becoming baseline

Needed for:

- deciding whether to keep or discard current service code
- preventing low-quality assumptions from solidifying into the main branch
- making docs the short-term source of truth

Options still open:

- keep only documentation on the main branch for now
- keep docs plus minimal verified repo skeleton only
- keep current code and revise incrementally
