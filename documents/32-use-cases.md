# Use Cases

## UC-1 Browse and Extract

1. The agent opens a page through MCP.
2. The agent requests `extract_page`.
3. MCP collects current page content and official labels.
4. The normalizer returns `semantic_summary`, `actionable_view`, and artifact references.
5. The agent chooses the next action.

## UC-2 Multi-Step Login Workflow

1. The agent opens a login page.
2. The agent uses official MCP labels to fill inputs and submit.
3. The browser session is reused for follow-up steps.
4. If page understanding is needed, the agent runs `extract_page`.

## UC-3 Verify a Suspicious Interpretation

1. The agent receives normalized output.
2. The agent detects ambiguity or low confidence.
3. The agent retrieves a specific artifact reference.
4. The agent compares artifact content against browser truth and proceeds or re-extracts.

## UC-4 Continue After Page Change

1. The agent performs a page-changing action such as click or navigation.
2. Prior labels are treated as stale.
3. The agent runs a fresh `extract_page`.
4. The agent uses the refreshed MCP labels for the next action.

## UC-5 Browser Egress Isolation Experiment

1. `steel-browser` runs with the `warp` sidecar candidate.
2. MCP and normalizer remain outside the browser egress path.
3. The team validates whether browser behavior remains stable.

Reference docs:

- [09-dev-topology.md](/Users/soo/workspace/steel-platform/documents/09-dev-topology.md)
- [12-artifact-policy.md](/Users/soo/workspace/steel-platform/documents/12-artifact-policy.md)
- [22-warp-egress-strategy.md](/Users/soo/workspace/steel-platform/documents/22-warp-egress-strategy.md)
