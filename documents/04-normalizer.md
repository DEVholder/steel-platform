# Content Normalizer

Goal:

- reduce token waste without losing action accuracy

Current MVP model choice:

- default SLM: `ReaderLM-v2`

Model strategy:

- MVP uses `ReaderLM-v2` as the primary HTML understanding and conversion model
- the normalizer should not hardcode a single-model implementation
- model invocation should sit behind an adapter layer so future models can be added without changing the API contract

The normalizer should remove:

- scripts
- styles
- tracking markup
- repeated layout boilerplate
- low-value attributes

The normalizer should preserve:

- page title
- main visible content
- links and hrefs
- buttons
- inputs and forms
- labels, names, types, visibility, disabled state
- stable ids or selector hints where possible

Outputs:

- `semantic_summary` for reasoning
- `actionable_view` for execution
- artifact references for fallback

Hard rules:

- do not invent actionable elements
- do not let semantic guesses override browser truth
- keep actionable output conservative

Implementation direction:

- use `ReaderLM-v2` for HTML-to-Markdown and structured condensation
- preserve raw HTML as an artifact, but send a lightly cleaned HTML variant to the model for primary inference
- preserve a stable normalizer output schema even if the backend model changes later

Read next:

- API payloads: [05-api.md](/Users/soo/workspace/steel-platform/documents/05-api.md)
- persistence of normalized output: [06-data-model.md](/Users/soo/workspace/steel-platform/documents/06-data-model.md)
