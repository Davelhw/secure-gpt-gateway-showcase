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

## Endpoint Access Matrix

| Area            | Endpoint                     | Purpose                                                     | Auth Required | Demo Access           |
| --------------- | ---------------------------- | ----------------------------------------------------------- | ------------- | --------------------- |
| Authentication  | `POST /api/auth/login`       | Establish a demo session and return caller identity context | No            | Allowed               |
| User context    | `GET /api/me`                | Return the current authenticated user and role information  | Yes           | Allowed               |
| Gateway chat    | `POST /api/gateway/chat`     | Submit a controlled AI request through the gateway          | Yes           | Limited               |
| Usage reporting | `GET /api/usage/summary`     | Review usage and high-level consumption summaries           | Yes           | Allowed               |
| Audit logs      | `GET /api/audit-logs`        | View governance-relevant request and decision records       | Yes           | Read-only             |
| Admin providers | `GET /api/admin/providers`   | Review configured provider entries and status metadata      | Yes           | Read-only             |
| Admin policies  | `POST /api/admin/policies`   | Create or update policy configuration                       | Yes           | Disabled or simulated |
| Rate limits     | `GET /api/admin/rate-limits` | Review configured rate-limit and quota settings             | Yes           | Read-only             |

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

## Common Error Responses

### 401 Unauthorized

```json
{
  "statusCode": 401,
  "error": "Unauthorized",
  "message": "Authentication is required for this endpoint."
}
```

### 403 Forbidden

```json
{
  "statusCode": 403,
  "error": "Forbidden",
  "message": "Your role does not have access to this resource."
}
```

### 429 Rate Limited

```json
{
  "statusCode": 429,
  "error": "Too Many Requests",
  "message": "Rate limit exceeded for the current time window."
}
```

### 422 Policy Blocked

```json
{
  "statusCode": 422,
  "error": "PolicyBlocked",
  "message": "The request was blocked by gateway policy.",
  "decision": "blocked"
}
```

### 502 Provider Error

```json
{
  "statusCode": 502,
  "error": "ProviderError",
  "message": "The upstream AI provider could not complete the request."
}
```

## Demo API Notes

- The public demo may use limited real AI calls or simulated provider responses.
- Admin write actions may be disabled or simulated.
- Public demo users should not assume every documented endpoint is writable.
- API examples are illustrative and may be narrower in the public demo.

## Notes on Safe Public Documentation

- No real API keys, secrets, tokens, or private URLs are included here.
- Example payloads are illustrative and use placeholder values.
- Public demo capabilities may be narrower than the internal private implementation.
