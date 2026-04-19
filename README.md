# Incident Response Playbook

A production-ready collection of runbooks, escalation frameworks, communication templates, and post-incident review guides for SaaS and CDN operations teams.

Built from 13+ years of incident response experience across CDN infrastructure (Fastly), fintech (APEXX Global), and enterprise SaaS (RM Plc).

---

## What's in here

| Directory | Contents |
|---|---|
| [`runbooks/p1/`](./runbooks/p1/) | P1 (Critical) runbooks — full triage and response procedures |
| [`runbooks/p2/`](./runbooks/p2/) | P2 (High) runbooks |
| [`runbooks/p3/`](./runbooks/p3/) | P3 (Medium) runbooks |
| [`escalation/`](./escalation/) | Escalation matrix and on-call decision trees |
| [`comms/customer-facing/`](./comms/customer-facing/) | Customer notification templates by severity |
| [`comms/internal/`](./comms/internal/) | Internal bridge and stakeholder update templates |
| [`rca/`](./rca/) | Post-incident review templates and a worked example |
| [`templates/`](./templates/) | Blank runbook template for new incident types |

---

## Severity definitions

| Severity | Label | Customer impact | Response SLA | Examples |
|---|---|---|---|---|
| **P1** | Critical | Service down or data loss for all/major customers | 15 min | CDN total outage, payment processing down, TLS failure on all origins |
| **P2** | High | Significant degradation for a subset of customers | 30 min | Increased error rates, latency spikes, single-region failure |
| **P3** | Medium | Minor degradation, workaround available | 2 hrs | Slow dashboard, non-critical feature unavailable, isolated errors |
| **P4** | Low | Cosmetic or negligible impact | Next business day | UI glitch, documentation error, minor config drift |

---

## How to use this playbook

1. **Declare severity** using the definitions above as soon as a possible incident is detected.
2. **Open the relevant runbook** for the incident type from `runbooks/p{severity}/`.
3. **Assign roles** per the escalation matrix in `escalation/`.
4. **Send the initial comms** using the appropriate template from `comms/`.
5. **Run the RCA** within 48 hours of resolution using the template in `rca/`.

---

## Principles

- **Declare early, downgrade later.** It is always better to over-declare and stand down than to under-declare and scramble.
- **Communicate before you have answers.** Customers and stakeholders need to know you're aware. Silence is worse than uncertainty.
- **Blameless by default.** The RCA process is about systems and processes, not individuals. Focus on what failed, not who.
- **Document everything in real time.** Ticket timeline, Slack thread, or bridge notes — decisions and actions must be captured as they happen.

---

## Runbooks available

### P1 — Critical
- [CDN total outage](./runbooks/p1/cdn-total-outage.md)
- [TLS certificate failure](./runbooks/p1/tls-certificate-failure.md) *(coming soon)*
- [Payment gateway down](./runbooks/p1/payment-gateway-down.md) *(coming soon)*

### P2 — High
- [Elevated error rates](./runbooks/p2/elevated-error-rates.md) *(coming soon)*
- [Single-region latency spike](./runbooks/p2/single-region-latency.md) *(coming soon)*

### P3 — Medium
- [Dashboard performance degradation](./runbooks/p3/dashboard-degradation.md) *(coming soon)*

---

## Contributing

If you're forking this for your team:
1. Replace severity SLAs with your actual contractual SLAs.
2. Update the escalation matrix with real names, Slack handles, and PagerDuty rotations.
3. Tailor comms templates to your company's tone of voice.
4. Run a tabletop exercise against one runbook before relying on it in production.

---

*Maintained by Phil Carroll-O'Kane · [carrollokane.com](https://carrollokane.com) · [github.com/philcodex](https://github.com/philcodex)*
