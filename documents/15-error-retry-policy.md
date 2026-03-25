# Error Handling and Retry Policy

The system should distinguish between:

- browser execution failures
- normalizer failures
- session failures
- invalid user or agent requests

MVP handling rules:

- `open`, `click`, `type`, `wait`, and `extract` should return structured errors
- every failure should carry `request_id`
- retries should happen only where the failure mode is likely transient

Examples of transient failures:

- temporary browser unavailability
- page still loading during wait
- short-lived network failure between containers

Examples of non-transient failures:

- invalid target element
- malformed request payload
- unsupported action

Fallback rule:

- if normalizer fails, the system should preserve artifact references and return a clear failure instead of silently passing raw HTML as the default success payload

Read next:

- API envelope: [05-api.md](/Users/soo/workspace/steel-platform/documents/05-api.md)
- artifact fallback: [12-artifact-policy.md](/Users/soo/workspace/steel-platform/documents/12-artifact-policy.md)
