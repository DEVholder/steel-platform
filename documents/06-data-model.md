# Data Model

Minimum persistent entities:

- `BrowserSession`
- `BrowserAction`
- `NormalizedPage`
- `Artifact`
- `SessionCookieStore`

Recommended MVP store:

- SQLite

Entity intent:

- `BrowserSession`: reusable session identity and metadata
- `BrowserAction`: one issued browser command
- `NormalizedPage`: what the agent actually received
- `Artifact`: screenshot, raw HTML, and similar references
- `SessionCookieStore`: persisted cookie state

Read next:

- API interaction points: [05-api.md](/Users/soo/workspace/steel-platform/documents/05-api.md)
- operational handling: [08-operations.md](/Users/soo/workspace/steel-platform/documents/08-operations.md)
