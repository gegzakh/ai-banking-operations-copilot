# AI Banking Operations Copilot — Business Requirements

**Document type:** Business Requirements Document (BRD)  
**Target state:** Production bank-operations platform, not the public demonstration  
**Status:** Baseline for discovery, estimation, control design, and phased delivery  
**Version:** 1.0 — 3 September 2026

## 1. Executive summary

The AI Banking Operations Copilot helps operations, SRE, NOC, application, payments, core-banking, and service-management teams convert fragmented operational signals into an evidence-linked, prioritized response. It correlates incidents, alerts, metrics, logs, traces, changes, deployments, business services, transaction outcomes, queues, and runbooks; proposes likely causes and safe next actions; coordinates human approvals; and prepares reliable stakeholder communications and shift handovers.

The production product must replace the demo's synthetic client-side responses with real-time integrations, governed service topology, secure retrieval, controlled automation, case/incident persistence, evaluation, and audit. It is a decision-support and orchestration platform: accountable operators remain in control of material actions.

## 2. Problems to solve

1. Operators monitor many tools and receive duplicated, noisy, or weakly prioritized alerts.
2. Technical symptoms are not connected quickly to customer journeys, transaction success, financial/regulatory exposure, SLAs, and business owners.
3. Root-cause investigation depends on individual knowledge and manual cross-tool searches.
4. Recent changes, dependency health, and historical incident patterns are difficult to correlate under pressure.
5. Runbooks are fragmented or stale, and operators cannot easily know which procedure applies.
6. Incident actions, approvals, evidence, and communications are spread across chat, tickets, calls, and dashboards.
7. Shift handovers lose context, decisions, hypotheses, pending checkpoints, and ownership.
8. Uncontrolled generative AI can hallucinate causes or actions, disclose sensitive data, or encourage unsafe production changes.

## 3. Product vision

Create an evidence-first operations command layer that helps the bank answer three questions rapidly and safely: **What needs attention now? Why is it happening? What approved action should happen next?**

## 4. Business objectives and success measures

| Objective | Target measure after rollout |
|---|---|
| Reduce noise | 50% reduction in alerts presented as separate actionable cases through correlation/deduplication |
| Improve detection/triage | 30% reduction in median time to acknowledge and establish business impact |
| Accelerate diagnosis | 25% reduction in median time to validated probable cause for supported services |
| Improve recovery | 20% reduction in MTTR without increasing change-failure or recurrence rate |
| Increase runbook discipline | At least 90% of material actions linked to an approved runbook step or authorized exception |
| Strengthen handovers | 100% of open critical/high incidents included in acknowledged structured handover |
| Maintain safety | Zero autonomous high-impact actions outside pre-approved policy; all AI claims/actions auditable |
| Improve learning | Post-incident actions and runbook updates tracked to closure with effectiveness evidence |

Targets must be baselined and approved per service tier.

## 5. Stakeholders and personas

| Persona | Primary need |
|---|---|
| NOC/operations analyst | Prioritized work queue, context, evidence, owners, and guided actions |
| Incident commander | Business impact, timeline, hypotheses, decisions, actions, communications, and escalation |
| SRE/platform engineer | Metrics/logs/traces, dependency/change correlation, SLOs, and safe automation |
| Application/core/payment owner | Domain context, technical diagnosis, rollback/fix options, and customer impact |
| Service desk | Clear status, known issue, workaround, and escalation route |
| Business service owner | Customer/business impact, decisions, recovery forecast, and risk acceptance |
| Change/release manager | Correlation to deployments/configuration, rollback authority, and change evidence |
| Security/fraud/financial-crime operations | Controlled collaboration where operational anomalies may be security or financial-risk events |
| Risk/compliance/resilience | Regulatory/materiality triggers, continuity, records, and operational risk reporting |
| Executive/communications stakeholder | Accurate, approved, audience-specific status and recovery updates |
| AI governance/model risk | Use-case approval, evaluation, monitoring, incident, provider, and change controls |

## 6. Business scope

### 6.1 In scope

- Unified operational work queue across alerts, incidents, service health, transaction KPIs, and backlog indicators.
- Correlation, deduplication, anomaly context, severity/priority recommendation, and business-impact calculation.
- Evidence-linked investigation of metrics, logs, traces, changes, topology, past incidents, and knowledge.
- Hypothesis management and explainable probable-cause recommendations with confidence and contradictory evidence.
- Approved runbooks, guided execution, action preparation, human approval, automation policy, and verification.
- Incident command, timeline, collaboration, tasks, checkpoints, escalation, and ownership.
- Customer/business/regulatory materiality context and routing to specialized processes.
- Draft communications, stakeholder updates, incident summaries, and shift handovers with approval.
- Post-incident review, learning, action tracking, runbook improvement, and analytics.
- Enterprise identity, access, audit, privacy, data retention, AI governance, observability, and integrations.

### 6.2 Out of scope for the initial production release

- Replacing monitoring/APM, SIEM, ITSM, architecture inventory, CI/CD, chat, or paging products.
- Allowing an LLM to execute unrestricted production commands.
- Treating correlation or generated explanations as confirmed root cause without operator validation.
- Combining security/fraud/customer-sensitive cases into general operations views without policy and need-to-know access.

## 7. Required business capabilities

1. **Signal ingestion and normalization** from monitoring, logs, traces, business KPIs, ITSM, changes, deployments, and topology.
2. **Correlation and prioritization** by service, time, symptom, topology, change, customer impact, financial exposure, SLA, and recurrence.
3. **Operational context** with owners, criticality, dependencies, SLOs, runbooks, recent changes, maintenance, and known errors.
4. **Evidence-first copilot** that cites source observations, distinguishes facts/hypotheses, and exposes uncertainty.
5. **Human-controlled response** with runbook steps, risk level, authorization, maker-checker, simulation, execution, and outcome verification.
6. **Incident coordination** through structured roles, timeline, actions, checkpoints, communications, and handover.
7. **Business/regulatory escalation** for payment, security, fraud, privacy, material ICT, and customer-impact events.
8. **Knowledge and learning** from approved runbooks, known errors, post-incident reviews, and resolved cases.
9. **Governance and assurance** for AI behavior, access, data, provider, prompts, tools, evaluation, and audit.

## 8. Core business processes

### 8.1 Detect and triage

The platform receives signals, groups related events, identifies the probable affected service, calculates urgency and business impact, and creates or updates an operational case. An operator confirms/changes severity, ownership, and incident status.

### 8.2 Investigate and diagnose

The operator asks a question or follows a guided investigation. The copilot retrieves authorized live/historical evidence, constructs a timeline, identifies recent changes and dependency anomalies, proposes hypotheses, shows supporting/contradicting evidence, and recommends validation steps. A human confirms the probable cause.

### 8.3 Respond and recover

The platform selects an approved runbook, checks prerequisites and action risk, prepares commands/API changes, obtains required authorization, executes only through scoped automation when permitted, captures output, and verifies service/customer recovery against predefined success and rollback criteria.

### 8.4 Communicate and hand over

The platform drafts audience-specific updates from confirmed facts, then requires authorized review before distribution. At shift change, open cases, impact, timeline, decisions, actions, risks, checkpoints, and owners are compiled and acknowledged by the receiving shift.

### 8.5 Learn

Confirmed cause, resolution, evidence, false alerts, runbook effectiveness, and follow-up actions feed post-incident review and controlled knowledge updates. AI quality and operator outcomes are monitored separately.

## 9. Business rules

1. AI-generated statements must identify supporting evidence and confidence; facts, hypotheses, recommendations, and operator confirmations must remain distinct.
2. Missing or contradictory evidence must be visible; the copilot must be able to state that it cannot determine a cause.
3. Incident priority combines service criticality, customer/transaction impact, financial/regulatory exposure, duration, redundancy, and SLA—not alert severity alone.
4. Production actions require a versioned approved runbook or an authorized documented exception.
5. Action authorization depends on environment, service tier, blast radius, reversibility, action class, time, and operator role.
6. High-impact/irreversible actions require human approval and, where configured, maker-checker; no conversational prompt can bypass policy.
7. Every action must capture inputs, approver, executor, output, timestamps, result, verification, and rollback status.
8. External communications use confirmed facts and authorized templates and require approval.
9. Sensitive evidence must remain protected in search, prompts, output, exports, and collaboration channels.
10. Learning content does not become approved knowledge or a runbook without owner review/versioning.

## 10. Security, privacy, and AI governance outcomes

- Enterprise SSO/MFA, least privilege, just-in-time privileged access, segregation of duties, and environment/service scopes.
- Read-only tool access by default; separately approved execution credentials with allow-listed operations and short-lived tokens.
- Prompt injection and untrusted-log/content defenses; secrets/PII masking; provider allow-lists; no training on bank data.
- Full tool-call, retrieval, model/version, prompt-template, output, approval, action, and communication audit.
- AI evaluation for evidence faithfulness, unsafe action refusal, sensitive-data leakage, priority/impact accuracy, and operator usefulness.
- Kill switch, graceful non-AI fallback, quotas, model/provider failover policy, and incident response for the copilot itself.

## 11. Risks and mitigations

| Risk | Required mitigation |
|---|---|
| Hallucinated root cause | Evidence citations, contradiction display, confidence, validation steps, human confirmation |
| Unsafe automation | Read-only default, allow-lists, action classes, approvals, dry-run, rollback, verification |
| Sensitive data leakage | Authorization-aware retrieval, redaction, DLP, approved providers/regions, output controls |
| Alert correlation hides events | Explainable grouping, raw-event access, recall testing, operator split/merge, audit |
| Incorrect business impact | Governed service map, as-of topology, confidence, owner confirmation, reconciliation |
| Automation dependency during outage | Degraded/manual mode, cached approved runbooks, independent access path |
| Operators over-rely on AI | Training, uncertainty, required confirmations, sampling, quality dashboards |

## 12. Business acceptance criteria

1. A real incident can be traced from source signals to case, business impact, investigation evidence, confirmed cause, approved action, recovery verification, communication, handover, and post-incident actions.
2. Unauthorized users cannot retrieve restricted logs, customer/security data, incidents, actions, or AI context through any channel.
3. The copilot refuses unsupported claims/actions and every material answer cites accessible evidence.
4. Action policy reliably prevents unauthorized, high-impact, wrong-environment, expired-runbook, or missing-approval execution.
5. Correlation, prioritization, diagnosis support, and action recommendations meet agreed offline and production evaluation thresholds.
6. Degraded/manual operating procedures work when the copilot, model provider, or one integration is unavailable.

## 13. Delivery approach

1. Read-only operational context and case workflow for selected non-critical services.
2. Evidence-grounded investigation, handover, and communications under human approval.
3. Broader service coverage, business-impact and regulatory routing.
4. Low-risk approved automation with verification and rollback.
5. Advanced learning, proactive detection, and optimization after safety/quality measures are stable.

