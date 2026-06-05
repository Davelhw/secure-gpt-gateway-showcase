# Roadmap

## Current Showcase Scope

The current showcase scope focuses on demonstrating the core gateway pattern rather than presenting a fully expanded enterprise platform. The emphasis is on controlled request routing, governance-aware design, admin visibility, and a public demonstration boundary that is technically credible.

## Near-Term Improvements

Realistic near-term improvements include:

- Sharpening dashboard views for usage and audit summaries
- Expanding policy-management workflows
- Improving provider health visibility and operational status reporting
- Strengthening demo environment observability
- Refining quota and cost-reporting granularity

## Future Pipeline

The future roadmap is intentionally practical. These items extend the existing gateway and governance model rather than replacing it.

| Area                                      | Planned direction                                                    |
| ----------------------------------------- | -------------------------------------------------------------------- |
| Machine-learning-assisted data governance | Use classification and detection signals to support policy decisions |
| Sensitive data detection                  | Flag prompts that may contain protected or regulated content         |
| Prompt classification                     | Categorise usage by intent, risk type, or business context           |
| Risk scoring                              | Assign request risk scores to support review or escalation rules     |
| Automated policy recommendation           | Suggest safer default policies from observed usage patterns          |
| Anomaly detection for unusual AI usage    | Identify spikes, misuse signals, or unexpected behaviour             |
| Department-level cost allocation          | Attribute usage and spend by team, project, or department            |
| Multi-provider fallback                   | Route requests across providers for resilience or cost control       |
| Approval workflow for high-risk prompts   | Add review gates for elevated-risk requests                          |
| Enterprise identity provider integration  | Connect to broader SSO and directory environments                    |
| Advanced compliance dashboard             | Present governance status, trends, and policy outcomes more clearly  |

## Roadmap Positioning

This roadmap is intended to show a credible engineering direction. It avoids claiming capabilities that are not yet implemented and keeps the focus on features that naturally build on the gateway architecture already described in this repository.
