# spec-driven-demo

A spec-driven development example for a **Commercial Property Insurance Website Application** — demonstrating how to structure planning, architecture, security, and implementation workflows for FSI (Financial Services Industry) regulated workloads on Microsoft Azure.

## Overview

This project showcases a secure, conversion-focused web platform where:
- **Small/medium business owners** can get quotes and submit applications for commercial property coverage
- **Insurance brokers/agents** can manage multi-client submissions and delegated access
- **Underwriters** can review, triage, and move submissions through approval workflows
- **Policyholders** can track status, upload documents, and manage policy lifecycle

## Key Features (MVP)

- **Quote Intake Wizard** – Resumable sessions, step-level validation, property risk data capture
- **Document Management** – Drag/drop uploads, virus scanning, metadata tagging
- **Eligibility Screening** – Automated pass/refer/decline rules for immediate feedback
- **Underwriter Workbench** – Queue views, submission drill-down, notes, status transitions
- **Customer Portal** – Real-time status tracking, document requests, renewal reminders
- **Broker Features** – Multi-client submissions, bulk tools, delegated access
- **Claims FNOL** – First notice of loss initiation form
- **Notifications** – Email + in-app alerts
- **Audit Trail** – Immutable event log for compliance

## Project Structure

```
├── prd.md                          # Product Requirements Document
├── docs/
│   ├── PRD.yaml                    # Structured PRD metadata
│   └── plan/
│       └── plan-20260527-001/      # Active planning cycle
│           ├── plan.yaml           # Master plan
│           ├── plan-a.yaml         # Component A (e.g., Frontend)
│           ├── plan-b.yaml         # Component B (e.g., API)
│           ├── plan-c.yaml         # Component C (e.g., Infrastructure)
│           ├── research_findings_*.yaml  # Research outputs
│           ├── research-*.md       # Detailed research docs
│           └── logs/               # Execution logs
└── README.md                       # This file
```

## Development Approach

This project follows **spec-driven development**:

1. **Specs First** – Product requirements and architectural decisions documented before code
2. **Planning** – Multi-component decomposition, wave scheduling, risk analysis
3. **Research** – Architecture baseline, security/compliance controls, implementation strategy
4. **Implementation** – Code generation, testing, deployment automation
5. **Validation** – Security review, compliance verification, performance benchmarks

See [copilot-instructions.md](.github/copilot-instructions.md) for FSI standards and guardrails.

## Key Non-Functional Requirements

### Security
- MFA, RBAC, encryption in transit/at rest
- Customer-managed Key Vault integration
- Managed Identities (no shared secrets)
- API Management with WAF and rate limiting
- mTLS for service-to-service communication
- No PII in logs; correlation IDs for tracing

### Compliance
- Data retention policies enforced
- Audit trail for all data changes
- WCAG 2.1 AA accessibility
- Structured observability (Azure Monitor, Sentinel)

### Performance & Availability
- <2s page load for core pages; <5s for quote submissions
- 99.9% uptime SLA
- Resilience patterns (timeouts, retries, circuit breakers)
- Idempotency keys on state-changing APIs

### Scalability
- Async messaging (Azure Service Bus)
- Event-driven microservices
- Support for seasonal submission spikes

## Tech Stack

- **Cloud:** Microsoft Azure (single tenant, multi-region active/active for Tier-1)
- **Services:** C# (.NET 10), TypeScript, Azure Service Bus, Azure API Management, Azure Monitor
- **Infrastructure:** Bicep
- **Architecture:** Event-driven microservices with bounded contexts

## Getting Started

### Prerequisites
- .NET 10 SDK
- Node.js 20+
- Azure CLI
- Git

### Local Development

```bash
# Clone the repository
git clone https://github.com/yortch/spec-driven-demo.git
cd spec-driven-demo

# Review the PRD and planning docs
cat prd.md
ls -la docs/plan/plan-20260527-001/

# Follow setup instructions in component plans (plan-a.yaml, plan-b.yaml, etc.)
```

## Success Metrics

- Quote completion rate
- Quote-to-bind conversion rate
- Average underwriting turnaround time
- % submissions requiring rework due to missing data
- Portal adoption rate (brokers/policyholders)
- FNOL digital initiation rate

## Milestones

1. **Discovery & UX** (2–4 weeks) – workflows, wireframes, underwriting rule baseline
2. **MVP Build** (8–12 weeks) – quote flow, portal, underwriter queue, notifications
3. **Pilot Launch** (2–4 weeks) – controlled broker group, KPI baseline
4. **GA Release** (2 weeks) – production rollout, monitoring, support playbook

## Contributing

- All significant decisions must be captured as ADRs in `/docs/adr/`
- Security-sensitive code requires AppSec review
- See [copilot-instructions.md](.github/copilot-instructions.md) for FSI compliance guardrails

## Contact

For questions on architecture, security, or compliance requirements, refer to the planning docs in `docs/plan/` or reach out to the architecture team.

---

**Repository:** https://github.com/yortch/spec-driven-demo  
**Last Updated:** May 2026
