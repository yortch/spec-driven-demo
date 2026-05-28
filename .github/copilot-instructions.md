# Repository Copilot Instructions

These are always-on enterprise guardrails that shape
specs, designs, and generated code.

## Project Context

This repository hosts services for a regulated **Financial Services** environment.
All work must respect FSI compliance, security, and architectural standards.

- **Cloud platform:** Microsoft Azure (single tenant, multi-region active/active for Tier-1 services).
- **Primary languages:** C# (.NET 10) for services; TypeScript for web; Bicep for infrastructure.
- **Architecture style:** Event-driven microservices with bounded contexts. Sync via REST/gRPC; async via Azure Service Bus.

## Non-Negotiable Standards

### Security
- All PII and PCI data **must** be encrypted at rest using customer-managed keys in Azure Key Vault.
- All external calls require an authenticated identity (Managed Identity preferred; no shared secrets).
- Secrets, connection strings, and keys must come from Key Vault references — never from app settings or code.
- All public endpoints sit behind Azure API Management with WAF and rate limiting.
- TLS 1.2+ only. mTLS for service-to-service when crossing trust boundaries.

### Resilience
- All outbound calls require timeouts, retries with jitter, and circuit breakers (Polly in .NET).
- Idempotency keys required on all state-changing APIs.
- No unbounded queues, no synchronous fan-out > 3.

### Observability
- Structured logs to Azure Monitor / Sentinel. No PII in logs — use correlation IDs.
- OpenTelemetry traces on every request path.
- Every Tier-1 service exposes `/health/live` and `/health/ready`.

### Data
- All schemas versioned. Backwards-incompatible changes require an ADR and a migration plan.
- Audit events for every customer-data read/write, published to the `audit-events` topic.

## Architectural Decisions

- Reference the approved tech radar at `/docs/standards/tech-radar.md` before introducing a new library.
- Every significant decision must be captured as an ADR in `/docs/adr/` using the template at `/docs/adr/template.md`.
- Cross-team contracts live in `/contracts/` as OpenAPI or AsyncAPI specs and require review before code.

## How Copilot Should Work in This Repo

1. **Specs before code.** For any new feature, produce or update `spec.md`, then `plan.md`, then `tasks.md` before writing implementation code.
2. **Cite standards.** When a design choice is driven by a rule above, name the rule in the design doc.
3. **Surface gaps explicitly.** If a requirement conflicts with an FSI standard, stop and flag it — do not generate code that violates the standard.
4. **Prefer existing patterns.** Search the repo and `/docs/adr/` for prior decisions before proposing new ones.
5. **No fabricated facts.** Do not invent regulatory citations, library versions, or internal service names.

## Review Gates

- Spec → reviewed by product owner.
- Plan / design → reviewed by an architect (use the `architect` agent for a first pass).
- Code → reviewed by a peer; security-sensitive code requires AppSec sign-off.
