# Actionable View Schema

The actionable view should stay minimal and action-oriented.

The source of truth for action execution is the official MCP label set.

## Required fields for actionable elements

- `mcp_label`
- `kind`
- `text`
- `visible`
- `disabled`

## Optional fields by element type

Links may include:

- `href`

Inputs may include:

- `name`
- `type`
- `placeholder`

Forms may include:

- `submit_label`
- `fields`

## Schema rules

- `mcp_label` is the primary action key when available
- `selector_hint` is optional and should not be required in the MVP
- elements should be omitted rather than emitted with empty placeholder values
- stale labels must be refreshed through a new extract after page-changing actions

## Example

```json
{
  "buttons": [
    {
      "mcp_label": 12,
      "kind": "button",
      "text": "Login",
      "visible": true,
      "disabled": false
    }
  ],
  "inputs": [
    {
      "mcp_label": 7,
      "kind": "input",
      "text": "Email",
      "visible": true,
      "disabled": false,
      "name": "email",
      "type": "email",
      "placeholder": "you@example.com"
    }
  ]
}
```

Read next:

- MCP tool contracts: [26-mcp-tool-contracts.md](/Users/soo/workspace/steel-platform/documents/26-mcp-tool-contracts.md)
- normalizer contract: [11-normalizer-contract.md](/Users/soo/workspace/steel-platform/documents/11-normalizer-contract.md)
