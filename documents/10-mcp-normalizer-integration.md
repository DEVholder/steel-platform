# MCP to Normalizer Integration Spec

In the current development model, the AI agent talks to `steel-mcp-server`.

The MCP server is responsible for:

- issuing browser actions to `steel-browser`
- deciding when a result must be normalized
- forwarding extract-like browser output to `content-normalizer`
- returning normalized output to the agent by default

The normalizer is responsible for:

- calling `ReaderLM-v2` as the default model backend during MVP development
- preserving a stable output contract regardless of the underlying model
- preserving official MCP interaction labels when they are provided as input

Current rule:

- `extract` calls must pass through the normalizer

Default non-normalized actions:

- `open`
- `click`
- `type`
- `wait`
- `screenshot`

These actions should return status-oriented results unless explicitly expanded later.

Integration flow for `extract`:

1. agent calls MCP extract
2. MCP fetches current browser state from `steel-browser`
3. MCP collects the current interactive elements and their official MCP labels
4. MCP builds the normalizer request payload
5. MCP sends the payload to `content-normalizer`
6. normalizer returns `semantic_summary`, `actionable_view`, and `artifacts`
7. MCP returns the normalized result to the agent

Hard rules:

- raw HTML is not the default agent response
- the normalizer is mandatory for `extract`
- browser truth still comes from `steel-browser`
- artifact references must survive the pipeline
- the MCP layer should depend on the normalizer contract, not on `ReaderLM-v2` directly
- artifact inspection should happen through an explicit follow-up step when verification is needed
- the normalizer must not invent a separate action-label system when official MCP labels are available

Read next:

- normalizer payload shape: [11-normalizer-contract.md](/Users/soo/workspace/steel-platform/documents/11-normalizer-contract.md)
- raw artifact policy: [12-artifact-policy.md](/Users/soo/workspace/steel-platform/documents/12-artifact-policy.md)
