# Anti-Abuse and Access Policy

The platform should reduce the chance of account, IP, or automation blocks without implementing CAPTCHA bypass or anti-bot evasion features.

Allowed operating principles:

- prefer official APIs when available
- respect site terms, access controls, and rate limits
- use conservative request pacing
- back off quickly after challenge pages or repeated failures
- cache and reuse prior results where safe
- reuse valid sessions instead of creating unnecessary fresh sessions
- keep a human-in-the-loop path for login or challenge handling when required

Required safeguards:

- detect challenge or block pages and stop escalation
- avoid infinite retries
- log domains with repeated blocks
- support per-site allowlists and deny rules
- make request pacing configurable per workflow or site

Operational guidance:

- if a site starts challenging or blocking requests, reduce activity and investigate rather than increasing automation pressure
- if stable automation is critical, seek an approved integration path with the site owner

Out of scope:

- CAPTCHA solving services
- anti-bot bypass playbooks
- IP rotation strategies intended to defeat site protections

Read next:

- security policy: [17-security-access.md](/Users/soo/workspace/steel-platform/documents/17-security-access.md)
- operations baseline: [08-operations.md](/Users/soo/workspace/steel-platform/documents/08-operations.md)
