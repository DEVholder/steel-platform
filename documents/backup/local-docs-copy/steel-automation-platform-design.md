# Steel Automation Platform Design

## 1. Overview

This project is not just a replacement for Playwright or a simple deployment of Steel Browser.

It is better understood as a browser automation platform with the following goals:

- improve reliability for real-world automation tasks that often fail in plain Playwright
- make browser automation easier for AI agents to use
- reduce token waste by preprocessing browser output before sending it to larger models
- reduce page noise such as tracking scripts, boilerplate markup, and irrelevant attributes before agent reasoning
- centralize browser execution on the home server

In short, the system should provide a stable browser runtime, an agent-friendly control layer, and a content optimization layer.

## 2. Why This Exists

Playwright is powerful, but in practical automation it often runs into issues such as:

- CAPTCHA or anti-bot friction
- unstable login/session handling
- brittle flows on complex sites
- noisy raw HTML that wastes LLM tokens

Steel Browser helps with the browser/runtime side of the problem, but it does not by itself define the whole service architecture we want.

The target system is therefore broader than:

- "just use Playwright"
- "just run Steel Browser"
- "just expose Steel MCP"

Instead, the goal is to build a full browser automation service for AI agents.

## 3. Core Product Definition

The project should be treated as a layered platform:

1. Browser Runtime Layer
2. Agent Control Layer
3. Session and State Layer
4. Content Normalization Layer
5. Optional Local SLM Reasoning Layer

This makes the service more than a browser wrapper. It becomes an automation backend that can support multiple AI-driven workflows.

## 4. High-Level Architecture

### 4.1 Steel Browser

`steel-browser` is the core execution engine.

Responsibilities:

- run persistent browser sessions
- handle automation-resistant sites better than plain local Playwright in many cases
- provide a stable remote browser API
- support operational debugging

Deployment model:

- run as a Docker container on the k12 home server
- expose API through Nginx Proxy Manager
- keep DevTools port private for internal debugging

Recommended port strategy:

- `3000`: main Steel Browser API
- `9223`: local-only DevTools/debug access

### 4.2 Agent Control Layer

This layer is what AI agents actually talk to.

Options:

- direct Steel Browser API wrapper
- MCP server
- custom control gateway that exposes higher-level browser actions

Important note:

`steel-mcp-server` is useful when the agent ecosystem expects MCP, but it is not the entire platform by itself. It is an adapter layer.

For remote multi-agent usage, the control layer should ideally expose stable, higher-level actions such as:

- open page
- click element
- type into field
- wait for selector or state
- capture screenshot
- extract main content
- inspect important network activity

### 4.3 Session and State Layer

If this service is meant to be a practical Playwright alternative, session management is essential.

Responsibilities:

- cookie persistence
- account/session reuse
- login state tracking
- auth expiry detection
- retry and recovery policies
- proxy or fingerprint policy storage

Without this layer, the service remains a thin browser wrapper rather than a robust automation platform.

### 4.4 Content Normalization Layer

This is one of the most important value-add layers for AI usage.

Raw HTML is usually too verbose and expensive to feed directly into larger models.

Responsibilities:

- strip boilerplate
- remove tracking scripts, analytics tags, and low-value markup noise
- filter long, low-signal attributes and repeated layout wrappers when they do not matter for agent decisions
- extract main content
- convert page structure into compact JSON or Markdown
- isolate links, forms, buttons, tables, and major content blocks
- return agent-friendly summaries instead of full raw page source

This layer is a key token optimization mechanism.

Important clarification:

- Steel Browser is not itself the full content normalizer described in this document
- content normalization should be treated as a separate service or layer on top of browser execution
- a local SLM is optional at first and should be added only where it improves compression or classification

### 4.5 Local SLM Layer

The home server has 16GB RAM and a Radeon 780M iGPU, which makes it suitable for lightweight local models.

The local SLM should not try to replace the main reasoning model.

It should instead act as a preprocessing and compression engine.

Good uses:

- classify page type
- rank relevant content blocks
- summarize large extracted text
- transform normalized page data into compact JSON
- identify likely action candidates

Bad uses:

- full complex multi-step reasoning that belongs in a stronger external model

The most effective approach is:

- local SLM for cheap preprocessing
- external LLM only for hard reasoning

In the early stages of the project, the normalizer can rely mostly on rule-based extraction.

Examples:

- readability-style article extraction
- script and style stripping
- form, link, button, and table extraction
- repeated layout removal

The local SLM should be introduced only after the rule-based normalizer is already useful.

## 5. What This Is Not

This project should not be framed as:

- a simple Steel Browser container
- a permanent public MCP endpoint only
- a direct one-to-one Playwright clone

It is better framed as:

- an AI-ready browser automation service
- a centralized browser execution backend
- a token-aware web interaction pipeline

## 6. Recommended Initial Architecture

### Required Services

1. `steel-browser`
2. `control-gateway`
3. `content-normalizer`

### Strongly Recommended Services

4. `session-store`
5. `local-slm`

### Optional Services

6. job queue
7. logging/observability service
8. artifact storage for screenshots, traces, extracted content, and cookies

## 7. Recommended Service Responsibilities

### steel-browser

- browser execution
- remote browser sessions
- anti-bot improved runtime
- screenshots and low-level browser access

### control-gateway

- one stable endpoint for AI agents
- wrap Steel Browser into agent-oriented actions
- optionally expose MCP-compatible access
- enforce auth, rate limits, and request policy

### content-normalizer

- HTML to JSON/Markdown
- main content extraction
- structure cleanup
- removal of tracking, analytics, and boilerplate noise
- preservation of action-relevant UI structure
- token reduction before external model calls

### session-store

- persistent cookies
- session metadata
- login/account state
- reuse strategy across tasks

### local-slm

- lightweight summarization
- content compression
- block ranking
- page classification

## 8. Why This Beats a Simple Playwright Setup

Compared with plain Playwright, this architecture aims to provide:

- more durable browser sessions
- better handling of hostile or dynamic sites
- centralized browser runtime
- agent-compatible interfaces
- better debugging strategy
- lower token usage through preprocessing

The value is not in one single tool. The value is in combining:

- browser reliability
- AI-friendly control
- token-efficient extraction

## 9. Request Flow and Data Flow

The recommended end-to-end request flow is:

1. a user sends a task request to an AI agent
2. the AI agent decides that browser interaction is required
3. the agent sends a tool request through the `control-gateway` or `steel-mcp-server`
4. `steel-browser` performs the real browser actions
5. raw page results are collected from the browser runtime
6. `content-normalizer` converts those results into compact structured output
7. `local-slm`, if needed, performs additional compression or classification
8. the compact result is returned to the AI agent
9. the AI agent decides the next browser action or prepares the final answer for the user

Typical raw inputs collected from the browser layer:

- page URL and title
- raw HTML
- visible text
- links, buttons, inputs, and forms
- screenshots
- optional network or console summaries

Typical outputs returned to the agent:

- compact JSON
- Markdown summaries
- action candidates
- references to screenshots or raw HTML when deeper inspection is required

The intended flow is not:

- raw HTML directly to the agent every time

The intended flow is:

- user request
- agent reasoning
- browser action through Steel MCP or control layer
- browser result
- normalization
- optional low-cost compression
- result returned to agent
- next action or final response

In short, the most important interaction path is:

- `user -> AI agent -> Steel MCP/control layer -> steel-browser -> content-normalizer -> AI agent`

## 10. Core Goal: Noise Reduction Without Action Loss

The content normalizer should aggressively remove low-value noise, but it must not break the agent's ability to act on the page.

Examples of low-value noise:

- marketing and tracking JavaScript in `head` or `body`
- analytics and pixel code
- excessive inline styles
- long utility-class strings
- large hydration payloads
- repeated menu, footer, and wrapper markup
- low-signal attributes that do not affect action selection

Examples of information that should usually be preserved:

- button text
- link text and href
- form structure
- input labels, names, and types
- visibility and disabled state where available
- identifiers or selector hints needed for reliable follow-up actions

This means the normalizer is not just a summarizer. It is a controlled reduction layer.

## 11. Dual Representation Strategy

To avoid action corruption, the system should produce two different kinds of output:

1. semantic summary
2. actionable structured view

### Semantic Summary

This is for understanding.

It may include:

- page type
- main content Markdown
- important sections
- concise explanation of what the page is doing

This layer may use more aggressive simplification and optional SLM help.

### Actionable Structured View

This is for execution.

It should preserve action-relevant details such as:

- buttons
- links
- forms
- inputs
- selector hints
- visibility state
- disabled state

The agent may read the semantic summary to understand the page, but should rely on the actionable structured view when deciding concrete next actions.

This separation is critical to prevent the normalizer from polluting downstream browser commands.

## 12. Why MCP Alone Is Not the Whole Answer

MCP is useful, but it solves only one problem: how an agent talks to a tool.

It does not by itself solve:

- session persistence
- login recovery
- content compression
- token optimization
- debugging workflow
- multi-agent coordination

So even if `steel-mcp-server` is included, it should be treated as one layer in a larger system.

## 13. Token Optimization Strategy

Running MCP remotely does not meaningfully reduce LLM token usage by itself.

Token usage is mostly driven by:

- how much raw content is sent to the model
- how many tool iterations are performed
- how much redundant HTML or page noise is included

Therefore, the correct optimization strategy is:

1. use Steel Browser for reliable interaction
2. normalize HTML into compact structured output
3. use a local SLM to compress or classify content when useful
4. send only the minimum necessary data to the larger model

This is where the real cost reduction happens.

The main token savings should come from:

- removing raw script noise
- dropping repetitive layout markup
- converting large HTML trees into compact structured output
- only escalating to the larger model when needed

## 14. Deployment Strategy for the k12 Home Server

### Server Profile

- device: Gemtek k12 mini PC
- memory: 16GB RAM
- GPU: Radeon 780M iGPU

### Practical Fit

This hardware is a good fit for:

- always-on Steel Browser
- a lightweight API gateway
- a content normalization service
- a small local SLM for preprocessing

It is not ideal for:

- large general-purpose local LLM hosting as the primary reasoning engine

## 15. Proposed MVP

The MVP should focus on reliability first, then optimization.

### Phase 1

- deploy `steel-browser`
- expose it safely through Nginx Proxy Manager
- keep `9223` local-only

### Phase 2

- build `control-gateway`
- implement a small set of high-value actions:
  - open page
  - click
  - type
  - wait
  - screenshot
  - extract main content

### Phase 3

- build `content-normalizer`
- return compact JSON/Markdown instead of raw HTML
- explicitly separate semantic summary from actionable structured view

### Phase 4

- add `session-store`
- persist cookies and account state

### Phase 5

- add `local-slm`
- use it only for compression, classification, and extraction help

## 16. Suggested Technical Stack

### Browser Runtime

- Steel Browser in Docker

### Control Gateway

- Python FastAPI or Node.js

### Content Normalization

- Python service using:
  - trafilatura
  - readability-lxml
  - BeautifulSoup

### Session Store

- Redis for transient job/session coordination
- PostgreSQL or SQLite for durable metadata, depending on scale

### Local SLM

- Ollama or llama.cpp-based serving

## 17. Security and Exposure Model

Recommended exposure rules:

- expose only the main browser/API endpoint externally
- keep debug ports like `9223` local-only
- require authentication at the reverse proxy
- log agent actions and browser job metadata
- avoid exposing raw internal debug endpoints to the public internet

## 18. Final Conclusion

The project should be defined as a Steel-based browser automation platform for AI agents, not as a simple Playwright replacement.

Playwright replacement is one important use case, but the larger opportunity is:

- centralized browser execution
- better automation reliability
- agent-ready tooling
- token-aware content extraction

The recommended final platform vision is:

- `steel-browser` for execution
- `control-gateway` for agent access
- `session-store` for persistence
- `content-normalizer` for token efficiency
- `local-slm` as an optional low-cost preprocessing layer

That architecture is much stronger than simply running Playwright or exposing a raw browser endpoint.
