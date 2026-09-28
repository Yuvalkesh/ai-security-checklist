# AI Security Checklist

**Secure the workflow. Protect the keys. Verify the boundaries.**

A practical, vendor-neutral checklist from **FutureProof Agents** for teams deploying AI in the cloud, on their own servers, or on employee computers.

Start with three questions:

1. **Where are the credentials, and what can read them?**
2. **Which software runs, and who can change it?**
3. **Who can reach the system, and what can it do for them?**

Then test what happens if a model follows a malicious instruction, a dependency is compromised, or an execution boundary fails. Hosting location is one design choice; security also depends on identities, permissions, dependencies, data flows and containment.

## Choose your starting point

| What you need | Start here |
| --- | --- |
| A first conversation with the business and technical owners | [12 essential questions](QUICKSTART.md) |
| A complete implementation review | [60-control checklist](CHECKLIST.md) |
| A record of owners, evidence, findings and release approval | [Private assessment template](templates/assessment.md) |
| Practical tests using synthetic data | [Acceptance tests](docs/ACCEPTANCE-TESTS.md) |
| A design review before implementation | [Threat model and deployment profiles](docs/THREAT-MODEL.md) |
| A response to a suspected exposed key or compromised component | [Incident response playbook](docs/INCIDENT-RESPONSE.md) |
| Questions for an AI, hosting or integration supplier | [Vendor questionnaire](docs/VENDOR-QUESTIONNAIRE.md) |
| A record of a temporary risk exception | [Exception template](templates/risk-exception.md) |
| A reusable machine-readable control catalog | [controls.json](controls.json) |

## Use it with your team

1. Download or copy the checklist into your **private** project workspace.
2. Select the applicable deployment profiles: cloud, self-hosted, agents and retrieval (RAG).
3. Assign actual owners. Record each applicable control as Pass, Fail, Unknown or Exception, with dated evidence. Explain exclusions.
4. Resolve the **P0 launch gates** before release, or obtain a specific, time-limited risk exception from the accountable owner. Track P1 hardening with deadlines.
5. Repeat the relevant checks when permissions, integrations, models, dependencies or deployment boundaries change.

The Markdown checkboxes are portable. To use clickable GitHub task lists, copy the relevant content into an issue **in your own private repository**. The JSON catalog can feed internal review tools; it contains criteria, not a scanner or completed results.

[Download the project as a ZIP](https://github.com/Yuvalkesh/ai-security-checklist/archive/refs/heads/main.zip)

## What this covers

- Cloud APIs and managed AI services.
- Self-hosted inference and management endpoints.
- Agents, coding assistants, tools, plugins and MCP integrations.
- Retrieval indexes, conversation memory, caches and generated outputs.
- Credentials, software supply chains, execution isolation and shared storage.
- Monitoring, containment, credential revocation and clean recovery.

There is no installation, telemetry, external script or account connection required to read or use these documents. This repository does not assess your infrastructure automatically.

## Keep assessment evidence private

This repository is public. Use public issues only for improvements to the generic checklist. Keep keys, account identifiers, internal topology, vulnerability details, incident evidence and completed assessments in a restricted system.

The checklist is a practical baseline, not a certification or a substitute for a review of your actual architecture. Passing a control requires evidence for your configuration; a product name, security badge or enabled setting is not enough.

**Version:** 1.0.0 · **Reviewed:** September 28, 2026  
**Maintained by:** FutureProof Agents · [Change history](CHANGELOG.md) · [Contributing](CONTRIBUTING.md) · [Reuse terms](LICENSE)
