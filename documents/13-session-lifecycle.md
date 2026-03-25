# Session Lifecycle Spec

Session identity is represented by `session_id`.

The MVP session model should support:

- session creation
- session reuse
- cookie persistence
- last activity tracking

Minimum lifecycle:

1. create session
2. attach browser actions to the session
3. persist cookies and metadata
4. reuse the same session for follow-up actions
5. expire or discard the session when it is no longer valid

Current rules:

- multi-step browsing should prefer session reuse
- session state should survive across related requests where possible
- browser truth about auth state still comes from the live browser

Open details that still need final decisions:

- expiry timeout
- site-scope rules
- concurrent access rules
- re-auth behavior after session expiration

Read next:

- persistence entities: [06-data-model.md](/Users/soo/workspace/steel-platform/documents/06-data-model.md)
- error handling: [15-error-retry-policy.md](/Users/soo/workspace/steel-platform/documents/15-error-retry-policy.md)
