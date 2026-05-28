# spec-driven-demo

**A spec-driven development demo using the [GEM Team Plugin](https://github.com/github/awesome-copilot/blob/main/plugins/gem-team/README.md)** for a **Commercial Property Insurance Website Application**. This repository demonstrates end-to-end multi-agent orchestration for spec → design → implementation workflows in FSI (Financial Services Industry) regulated workloads on Microsoft Azure.

## Overview

**This repository is a working demo** of spec-driven development using the **GEM Team Plugin for GitHub Copilot**. It uses a real Commercial Property Insurance product specification to showcase:

- **Single-prompt orchestration** – One user prompt triggers coordinated multi-agent workflow
- **Spec as source of truth** – All design and code decisions flow from `prd.md`
- **FSI compliance patterns** – Security, audit, and data governance for regulated workloads
- **Modular agent workflows** – Separation of concerns: research, architecture, planning, implementation, testing, review

The application enables:
- **Small/medium business owners** to get quotes and submit applications for commercial property coverage
- **Insurance brokers/agents** to manage multi-client submissions and delegated access
- **Underwriters** to review, triage, and move submissions through approval workflows
- **Policyholders** to track status, upload documents, and manage policy lifecycle

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
└── README.md                       # This file
```

## GEM Team Plugin Setup

### Install the Plugin

The GEM Team Plugin provides multi-agent orchestration for spec-driven workflows. To install:

1. Open VS Code
2. Go to **Extensions** (Ctrl+Shift+X / Cmd+Shift+X)
3. Search for **"awesome-copilot"** or **"GEM Team"**
4. Click **Install** on the official GitHub awesome-copilot extension
5. Reload VS Code when prompted

Alternatively, install via GitHub CLI:
```bash
gh copilot plugin install github/awesome-copilot
```

### Kick Off the Spec-Driven Flow

Once the plugin is installed:

1. Open the **Copilot Chat** panel (Ctrl+Shift+I / Cmd+Shift+I)
2. Click the **Agent** dropdown (or icon) at the top of the chat input
3. Select **gem-orchestrator** from the list
4. In the chat input, paste or type the prompt:
   ```
   build this #file:prd.md
   ```
5. Press Enter. The orchestrator will:
   - Analyze the PRD using `gem-researcher`
   - Generate architecture with `gem-designer` and `architect` agents
   - Create implementation plan with `gem-planner`
   - Generate code via specialized implementer agents
   - Validate results with reviewer and tester agents

## Development Approach

This project follows **spec-driven development** with multi-agent coordination:

1. **Specs First** – PRD serves as single source of truth (see `#file:prd.md`)
2. **Research & Design** – Multi-agent analysis of requirements, architecture, security
3. **Planning** – DAG-based execution plan with component decomposition and wave scheduling
4. **Implementation** – Specialized agents handle frontend, backend, infra, tests
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

## Getting Started

### Quick Start with GEM Orchestrator

1. **Clone the repository**
   ```bash
   git clone https://github.com/yortch/spec-driven-demo.git
   cd spec-driven-demo
   ```

2. **Open in VS Code with GEM Team Plugin installed**
   ```bash
   code .
   ```

3. **Launch the orchestrated workflow in Copilot Chat**
   - Open Copilot Chat (Ctrl+Shift+I / Cmd+Shift+I)
   - Select **gem-orchestrator** from the agent dropdown
   - Type: `build this #file:prd.md`
   - Press Enter to trigger the full spec-driven pipeline with coordinated agents

### Manual Setup (without plugin)

If you prefer to work step-by-step without orchestration:

1. **Review the PRD**
   ```bash
   cat prd.md
   ```

2. **Use individual agents for each phase**
   - `@gem-researcher` – Explore and analyze requirements
   - `@architect` – Design architecture and create ADRs
   - `@gem-planner` – Create execution plan
   - `@gem-implementer` – Implement features via TDD
   - `@gem-reviewer` – Security audit and compliance check
   - `@gem-tester` – E2E and unit testing

3. **Prerequisites for local development**
   - Git
   - GitHub Copilot subscription

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

---

**Repository:** https://github.com/yortch/spec-driven-demo  
**Last Updated:** May 2026
