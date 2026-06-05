# Design Tradeoffs

## Why a Gateway Pattern Instead of Direct Provider Integration

Direct provider integration is faster for prototypes. A team can call an AI provider directly from a client or a small backend service and get useful results quickly.

The downside is that provider credentials, usage controls, logging behaviour, and policy enforcement tend to spread across multiple applications and services. That makes the system harder to govern and harder to change later.

A gateway adds one more layer to the request path, but it centralises the concerns that matter once AI usage moves beyond experimentation: governance, rate limits, audit logs, provider abstraction, and operational control. For systems that need maintainability, visibility, and controlled AI adoption, that tradeoff is worthwhile.

## Why Private Source with Public Documentation

The source code remains private because this project demonstrates security and governance patterns as much as it demonstrates application architecture.

Public documentation is sufficient for reviewers to understand the intent, architecture, API shape, and operational thinking behind the project. That provides a structured way to evaluate design decisions without exposing implementation details, secrets, security boundaries, or unnecessary abuse vectors.

For recruiters and technical reviewers, the documentation is the point: it shows how the system is framed, how the responsibilities are separated, and how the tradeoffs are reasoned through.

## Why Metadata or Redacted Prompt Logging Instead of Full Prompt Logging

Full prompt logging can help with debugging and review, but it also increases privacy, data retention, and compliance risk. In systems that may handle sensitive internal content, retaining full prompt bodies by default is often the wrong starting point.

Metadata-only or redacted logging reduces exposure while still supporting auditability. It allows the system to capture who made a request, when it happened, which route was used, and what policy or quota decision occurred without necessarily retaining sensitive input content.

The logging policy should be able to vary by environment and governance requirement. This is a practical balance between auditability and data minimisation.

## Why Provider Adapter Abstraction

Provider-specific request and response formats should not leak into client-facing features. If the rest of the platform depends directly on a provider's payload structure, the client layer becomes coupled to vendor-specific behaviour.

A provider adapter allows future support for multiple OpenAI-compatible providers and creates room for routing, fallback, migration, or cost-control strategies later. The tradeoff is additional internal abstraction, but the benefit is lower coupling and better long-term flexibility.

## Why Demo Restrictions Instead of Full Admin Access

A public demo should prove the concept without exposing operational control. That means real provider key editing, destructive actions, and unlimited AI usage should not be available publicly.

Some admin actions may be read-only, disabled, or simulated. That is an intentional tradeoff: the public environment remains useful for review without creating avoidable risk around cost, secrets, data exposure, or system integrity.

## Why JWT First with OAuth-Ready Design

JWT is a simple and practical starting point for a showcase or demo environment. It keeps the authentication model understandable without requiring a full identity integration story on day one.

OAuth or enterprise SSO can be added later for organisation-level identity integration. The important design point is to keep extension paths clear without overbuilding identity too early. That keeps the project focused without boxing it in.

## Why ML-Assisted Data Governance Is in the Roadmap, Not the First Release

ML-assisted prompt classification, risk scoring, sensitive data detection, and anomaly detection are useful future capabilities. They can make governance workflows more adaptive and more informative.

The first version should establish deterministic controls first:

- Authentication
- Authorization
- Rate limits
- Quota
- Policy rules
- Audit logging
- Provider abstraction

Deterministic controls are easier to explain, test, govern, and maintain. ML can support governance later, but it should not replace the foundation before the core control model is solid.

## Summary

The design favours control, clarity, maintainability, and safe public demonstration over maximum feature breadth.

These tradeoffs are intentional and reflect production-style thinking: establish clear boundaries, centralise control where it matters, and expand complexity only when the operational foundations are already in place.
