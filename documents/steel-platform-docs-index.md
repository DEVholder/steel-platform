# Steel Platform Docs Index

## Overview

This documentation set defines the Steel-based browser automation platform as a broader system than plain Playwright or a raw Steel Browser deployment.

Use this index as the starting point.

## Documents

1. [Platform Design](C:\Users\soo\Documents\steel-automation-platform-design.md)
   - high-level concept, goals, platform definition

2. [Architecture Overview](C:\Users\soo\Documents\steel-platform-architecture-overview.md)
   - system components, service boundaries, deployment model

3. [Request Flow and Sequence](C:\Users\soo\Documents\steel-platform-request-flow.md)
   - user to agent to MCP to browser to normalizer flow

4. [Content Normalizer Specification](C:\Users\soo\Documents\steel-content-normalizer-spec.md)
   - what the normalizer removes, preserves, and returns

5. [MCP and Browser Integration](C:\Users\soo\Documents\steel-mcp-browser-integration.md)
   - how Steel MCP, control gateway, and Steel Browser should interact

6. [Implementation Roadmap](C:\Users\soo\Documents\steel-platform-roadmap.md)
   - staged build plan from MVP to production

7. [Operations Runbook](C:\Users\soo\Documents\steel-platform-operations-runbook.md)
   - deployment, health checks, security, and debugging guidance

8. [Build Specification](C:\Users\soo\Documents\steel-platform-build-spec.md)
   - implementation-ready system specification with concrete component requirements

9. [API Contracts](C:\Users\soo\Documents\steel-platform-api-contracts.md)
   - proposed interfaces, payload shapes, and expected responses

10. [Repository Structure](C:\Users\soo\Documents\steel-platform-repo-structure.md)
   - recommended codebase layout and ownership by service

11. [Task Backlog](C:\Users\soo\Documents\steel-platform-task-backlog.md)
   - prioritized build tasks that an AI coding agent can execute

12. [Agent Handoff Guide](C:\Users\soo\Documents\steel-platform-agent-handoff.md)
   - direct instructions for another AI agent to implement the platform

13. [Product Requirements Document](C:\Users\soo\Documents\steel-platform-prd.md)
   - product goals, users, scope, and success criteria

14. [Requirements Specification](C:\Users\soo\Documents\steel-platform-requirements-spec.md)
   - functional and non-functional requirements

15. [Use Cases](C:\Users\soo\Documents\steel-platform-use-cases.md)
   - user and agent interaction scenarios

16. [Data Model and ER Diagram](C:\Users\soo\Documents\steel-platform-data-model.md)
   - proposed entities, relationships, and persistence design

17. [Architecture Decision Records](C:\Users\soo\Documents\steel-platform-adrs.md)
   - major architectural choices and rationale

## Recommended Reading Order

1. Platform Design
2. Architecture Overview
3. Request Flow and Sequence
4. Content Normalizer Specification
5. MCP and Browser Integration
6. Build Specification
7. API Contracts
8. Repository Structure
9. Task Backlog
10. Agent Handoff Guide
11. Product Requirements Document
12. Requirements Specification
13. Use Cases
14. Data Model and ER Diagram
15. Architecture Decision Records
16. Implementation Roadmap
17. Operations Runbook

## Summary

The platform should be understood as:

- a centralized browser execution backend
- an agent control system
- a token optimization pipeline
- a practical browser automation service for AI agents
- an implementation-ready engineering project with clear service boundaries and task sequencing
- a multi-document software design package that can guide implementation
