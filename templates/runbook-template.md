# P[X] Runbook: [Incident type]

**Severity:** P[X] — [Critical / High / Medium]
**Incident type:** [One-line description]
**Response SLA:** Declare within [X] minutes · First customer comms within [X] minutes
**Last reviewed:** [Month Year]
**Runbook owner:** [Role]

---

## Overview

[2–3 sentences describing this incident type and any key pre-triage guidance.]

---

## Roles and responsibilities

| Role | Responsibility | Assigned to |
|---|---|---|
| **Incident Commander (IC)** | Owns the response end-to-end. Makes all decisions. | On-call lead |
| **Technical Lead** | Drives triage and diagnosis. Reports findings to IC. | |
| **Comms Lead** | Drafts and sends all communications. | |
| **Scribe** | Documents all actions and timestamps in real time. | |

---

## Detection signals

You are likely dealing with this incident type if **two or more** of the following are true:

- [ ] [Signal 1]
- [ ] [Signal 2]
- [ ] [Signal 3]

---

## Step-by-step response

### Phase 1 — Declare and mobilise (0–[X] minutes)

- [ ] Declare [PX]. Post in `#incidents`:
  ```
  [PX DECLARED] [Incident type] — [timestamp UTC]
  IC: @[name] · Bridge: [link] · Ticket: [link]
  ```
- [ ] Open incident ticket
- [ ] Assign roles
- [ ] Notify relevant stakeholders

### Phase 2 — Triage and diagnosis

```bash
# Diagnostic command
[command]
```

- [ ] [Expected outcome A] → [next action]
- [ ] [Expected outcome B] → [alternative path]

### Phase 3 — Mitigation

- [ ] [Mitigation step]
- [ ] Verify recovery: [how to confirm]

### Phase 4 — Resolution

- [ ] Confirm recovery with Technical Lead
- [ ] Send all-clear
- [ ] Update ticket to Resolved
- [ ] Schedule RCA within 48 hours
- [ ] Close bridge

---

## Escalation path

```
[First responder] → ([condition]) → [Next escalation]
```

---

## Key metrics to capture

| Metric | Notes |
|---|---|
| Detection time | |
| Declaration time | |
| Mitigation applied | |
| Recovery confirmed | |
| Total duration | |

---

## Related documents

- [Escalation matrix](../../escalation/escalation-matrix.md)
- [Customer initial notification](../../comms/customer-facing/p1-initial-notification.md)
- [Blameless RCA template](../../rca/blameless-rca-template.md)

---

*Runbook owner: [Role] · Review cycle: Quarterly · Last reviewed: [Month Year]*
