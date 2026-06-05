# Demo Safety Boundaries

## Why the Public Demo Must Be Restricted

A public showcase environment must demonstrate architecture and product intent without behaving like an unrestricted production control plane. The demo needs to be safe to expose, inexpensive to operate, and resistant to misuse.

## Demo User Limitations

Public demo users should have access only to a constrained subset of the platform. They may be able to authenticate, view selected screens, submit limited gateway requests, and inspect sample reporting data, but they should not receive unrestricted operational control.

## Disabled Admin Actions

Administrative actions that could affect real infrastructure, secrets, or other users should be disabled, read-only, or simulated in the public demo.

## No Real Provider API Key Editing in Public Demo

The public demo must not expose real provider API key editing, secret storage interfaces, or configuration paths that could affect live integrations.

## No Unlimited AI Usage

Public access should never imply unrestricted model usage. The demo should be designed with bounded request volume, bounded throughput, and bounded cost exposure.

## Rate Limits and Quota Limits

Rate limits and quotas are part of the demo design, not just backend safeguards. They protect the environment from abuse while also illustrating the governance controls the platform is meant to provide.

## Sample or Seeded Audit Data

Audit and reporting screens may rely on sample, seeded, or carefully sanitised data so reviewers can understand the platform's operational model without exposing sensitive real-world records.

## No Destructive Actions

Destructive actions such as deleting providers, removing audit history, resetting live quotas, or changing production-like policies should not be available in the public demo.

## No Full Sensitive Prompt Retention

The demo should avoid retaining full sensitive prompt content. Where logging is needed for illustration, it should be redacted, sanitised, or reduced to metadata-only records.

## Screenshot Data Safety

Public demo screenshots should use synthetic data only.

- No real account numbers, addresses, phone numbers, customer records, provider keys, or tokens should appear in public screenshots.
- The current screenshot is intended as a synthetic demo case showing PII detection and redaction behaviour.

## Clear Demo Environment Banner

The user interface should make the environment status explicit with a clear demo banner or notice. Reviewers should understand that some actions are restricted, simulated, or intentionally non-persistent.

## Abuse Prevention Principles

The public demo should operate under a simple abuse-prevention model:

- Restrict who can do what
- Limit how much usage is allowed
- Avoid exposing real secrets or live administrative controls
- Record enough metadata to detect misuse
- Prefer reversible, low-risk interactions over persistent or destructive ones
