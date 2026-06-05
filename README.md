# Secure GPT Gateway

Secure GPT Gateway is a private-source AI governance and usage-control showcase. This public repository documents the architecture, design decisions, and demo boundaries for a controlled gateway that sits between client applications and AI providers.

Demo URL: https://secure-gpt.davelhw.com

Demo credentials: To be provided later

## Why I Built This

I initiated Secure GPT Gateway as a practical showcase after observing a familiar pattern: AI capabilities can be adopted quickly, but often without enough control around access, data exposure, cost visibility, auditability, and provider key management.

The goal is not to build another chatbot. The goal is to demonstrate how AI access can be treated as a governed platform capability with the same production engineering concerns that apply elsewhere in backend systems: authentication, authorization, policy enforcement, rate limiting, logging, operational review, and maintainability.

## What This Showcase Demonstrates

- API-first backend design
- Security-aware architecture
- Provider abstraction
- Governance and auditability
- Rate limiting and quota control
- Operational maintainability
- Demo-safe public exposure
- Clear documentation and technical communication

## Why This Project Exists

Many teams begin AI adoption by embedding provider API calls directly into internal tools or client-facing applications. That is fast to prototype, but it creates predictable control gaps around authentication, provider key exposure, usage visibility, rate limiting, quota enforcement, auditability, and policy consistency.

Secure GPT Gateway exists to show a more disciplined pattern: route AI access through a managed backend gateway where governance, usage control, and provider abstraction can be enforced centrally.

## What Secure GPT Gateway Serves

Secure GPT Gateway serves as a controlled access layer for organisations that want to adopt AI without giving every client application direct, unmanaged access to external AI providers.

It is intended for teams that need:

- A single integration surface for AI requests
- Authentication and access control before provider access
- Policy enforcement for allowed usage patterns
- Usage tracking, audit logging, and admin visibility
- Rate limiting and quota control for cost containment
- A provider abstraction layer that avoids vendor lock-in

## Key Features

- Central gateway for AI chat and related requests
- JWT-based authentication with OAuth-ready extension points
- Policy enforcement before provider execution
- Rate limiting and quota controls per user, role, or tenant
- Provider adapter pattern for OpenAI-compatible integrations
- Audit logging and usage tracking for governance review
- Administrative visibility into providers, policies, and limits
- Private-source implementation presented through public documentation only

## High-Level Architecture Summary

The platform is designed around a backend gateway API that brokers every AI request. A frontend dashboard provides user and administrator views. Authentication and authorization protect access. A policy engine evaluates requests before they reach the provider adapter layer. Rate limiting, quota control, audit logging, and usage tracking provide governance and operational visibility.

At a high level:

1. A user authenticates through the platform.
2. The client calls the gateway instead of the AI provider directly.
3. The gateway validates identity, role, policy, and usage limits.
4. A provider adapter forwards approved requests to a configured AI provider.
5. Usage and audit metadata are stored for review and reporting.

## Tech Stack Summary

| Area                 | Technology                             |
| -------------------- | -------------------------------------- |
| Language             | TypeScript                             |
| Backend              | NestJS                                 |
| Frontend             | Next.js                                |
| Relational storage   | PostgreSQL or MySQL                    |
| Caching and counters | Redis                                  |
| Containerisation     | Docker                                 |
| Edge / reverse proxy | NGINX                                  |
| Authentication       | JWT with OAuth-ready design            |
| Provider integration | OpenAI-compatible provider integration |

## Documentation Index

- [Project Background](./docs/01-project-background.md)
- [Architecture Design](./docs/02-architecture-design.md)
- [Design Tradeoffs](./docs/09-design-tradeoffs.md)
- [Development Lifecycle](./docs/03-development-lifecycle.md)
- [API Guide](./docs/04-api-guide.md)
- [Governance and Maintenance](./docs/05-governance-maintenance.md)
- [Roadmap](./docs/06-roadmap.md)
- [Demo Safety Boundaries](./docs/07-demo-safety-boundaries.md)
- [Reviewer Walkthrough](./docs/08-reviewer-walkthrough.md)

## Reviewer Quick Links

- [Start with Project Background](./docs/01-project-background.md)
- [Review Architecture Design](./docs/02-architecture-design.md)
- [Review Design Tradeoffs](./docs/09-design-tradeoffs.md)
- [Review API Guide](./docs/04-api-guide.md)
- [Review Governance and Maintenance](./docs/05-governance-maintenance.md)
- [Review Demo Safety Boundaries](./docs/07-demo-safety-boundaries.md)
- [Review Reviewer Walkthrough](./docs/08-reviewer-walkthrough.md)

## Source Code Note

- Source code is private.
- This public repository is provided as a technical showcase and architecture documentation.
