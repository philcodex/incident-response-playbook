# Escalation matrix

This matrix defines who to contact, when, and how — for every severity level.
Update names, handles, and contact details before deploying this playbook to your team.

---

## On-call rotation

| Role | Name | Slack | Phone | PagerDuty |
|---|---|---|---|---|
| Primary on-call | [Name] | @handle | +XX XXX XXX XXXX | [rotation link] |
| Secondary on-call | [Name] | @handle | +XX XXX XXX XXXX | [rotation link] |
| IR Lead | [Name] | @handle | +XX XXX XXX XXXX | [rotation link] |
| Head of Support | [Name] | @handle | +XX XXX XXX XXXX | — |
| VP Engineering | [Name] | @handle | +XX XXX XXX XXXX | — |

---

## Escalation by severity

### P1 — Critical

| Time elapsed | Action | Who |
|---|---|---|
| T+0 | Declare P1, open bridge, notify IR Lead | On-call engineer |
| T+5 min | If no IC response, page Secondary on-call | PagerDuty auto-escalation |
| T+15 min | Notify Head of Support via DM | IC |
| T+30 min | If unresolved, notify VP Engineering | IC |
| T+60 min | If unresolved, escalate to CTO. Review SLA breach risk | Head of Support |
| T+90 min | If customer SLA breach confirmed, notify Legal and Account Management | VP Engineering |

### P2 — High

| Time elapsed | Action | Who |
|---|---|---|
| T+0 | Declare P2, assign Technical Lead | On-call engineer |
| T+30 min | If unresolved, notify IR Lead | On-call engineer |
| T+2 hrs | If unresolved, escalate to Head of Support | IR Lead |

### P3 — Medium

| Time elapsed | Action | Who |
|---|---|---|
| T+0 | Log ticket, assign to queue | On-call engineer |
| T+2 hrs | If unresolved, flag in team standup | Engineer |
| Next business day | If still open, escalate to team lead | Engineer |

---

## CDN provider contacts

| Provider | Support portal | Emergency line | Account ID location |
|---|---|---|---|
| Fastly | support.fastly.com | On contract — check 1Password vault | Customer portal → Account settings |
| Cloudflare | dash.cloudflare.com/support | Enterprise: dedicated Slack channel | Dashboard → Account ID |
| Akamai | control.akamai.com | Luna Control Centre → Support case | Contract document |

**Rule:** For any P1 involving a third-party provider, open a ticket with them within the first 15 minutes.

---

## Decision tree: should I escalate?

```
Is the incident affecting ALL customers?
├── Yes → P1. Declare now. Do not investigate first.
└── No → Is it affecting MORE than 20% of customers?
    ├── Yes → Likely P2. Investigate for 15 min. If no quick fix, escalate.
    └── No → Is there a workaround available?
        ├── Yes → P3. Log and assign.
        └── No → P2. Notify IR Lead within 30 min.
```

---

*Review this matrix quarterly. Stale contact details are an incident risk.*
