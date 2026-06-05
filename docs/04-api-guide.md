# API Guide

## API Overview

Secure GPT Gateway exposes an application-facing API designed around controlled AI access rather than direct provider interaction. The route structure separates authentication, end-user gateway actions, operational reporting, and administrative controls.

This document describes the intended public-facing API shape for the showcase. It does not expose secrets, private infrastructure details, or internal-only implementation specifics.

## Route Groups

### Authentication Endpoints

Authentication endpoints establish the user session and return the identity context needed for protected routes.

### Gateway and Chat Endpoints

Gateway endpoints accept validated chat or prompt requests and route them through policy, quota, and provider layers before execution.

### Usage Summary Endpoints

Usage summary endpoints provide aggregate information about request counts, recent activity, and consumption trends appropriate to the caller's role.

### Audit Log Endpoints

Audit log endpoints expose governance-relevant records such as enforcement outcomes, blocked actions, and high-level request metadata.

### Admin Provider Endpoints

Administrative provider endpoints support controlled review of configured provider entries and their operational status. In a public demo, write actions may be disabled or simulated.

### Admin Policy Endpoints

Administrative policy endpoints support viewing or updating policy rules that shape model access, request restrictions, and escalation paths.

### Rate Limit and Quota Endpoints

These endpoints expose configured rate limits, quota definitions, or current usage state, depending on role and environment.

## Example Endpoint List

```text
POST /api/auth/login
GET  /api/me
POST /api/gateway/chat
GET  /api/usage/summary
GET  /api/audit-logs
GET  /api/admin/providers
POST /api/admin/policies
GET  /api/admin/rate-limits
```

Public demo users may not have access to all admin endpoints.

## Example Request and Response Payloads

### Login

Request:

```json
{
  "email": "reviewer@example.com",
  "password": "demo-password-placeholder"
}
```

Response:

```json
{
  "accessToken": "redacted-demo-token",
  "user": {
    "id": "usr_demo_001",
    "email": "reviewer@example.com",
    "role": "reviewer"
  }
}
```

### Get Current User

Response:

```json
{
  "id": "usr_demo_001",
  "email": "reviewer@example.com",
  "role": "reviewer",
  "permissions": ["gateway:chat", "usage:read"]
}
```

### Gateway Chat Request

Request:

```json
{
  "model": "gpt-4o-mini-compatible",
  "messages": [
    {
      "role": "user",
      "content": "Summarise the governance benefits of an AI gateway."
    }
  ],
  "context": {
    "project": "secure-gpt-gateway-showcase"
  }
}
```

Response:

```json
{
  "requestId": "req_demo_1024",
  "status": "completed",
  "provider": "openai-compatible",
  "usage": {
    "inputTokens": 24,
    "outputTokens": 112
  },
  "output": {
    "role": "assistant",
    "content": "A gateway centralises authentication, policy checks, rate limits, and auditability before provider access."
  }
}
```

### Usage Summary

Response:

```json
{
  "period": "30d",
  "requestCount": 184,
  "blockedCount": 7,
  "estimatedCost": 31.42,
  "topModels": [
    {
      "model": "gpt-4o-mini-compatible",
      "requestCount": 140
    }
  ]
}
```

### Audit Log List

Response:

```json
{
  "items": [
    {
      "id": "audit_001",
      "timestamp": "2026-06-05T10:15:00Z",
      "actor": "usr_demo_001",
      "action": "gateway.chat",
      "outcome": "allowed",
      "policyDecision": "pass"
    },
    {
      "id": "audit_002",
      "timestamp": "2026-06-05T10:16:00Z",
      "actor": "usr_demo_009",
      "action": "gateway.chat",
      "outcome": "blocked",
      "policyDecision": "quota_exceeded"
    }
  ]
}
```

## Notes on Safe Public Documentation

- No real API keys, secrets, tokens, or private URLs are included here.
- Example payloads are illustrative and use placeholder values.
- Public demo capabilities may be narrower than the internal private implementation.
