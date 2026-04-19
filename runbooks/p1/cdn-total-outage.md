# P1 Runbook: CDN Total Outage

**Severity:** P1 — Critical
**Incident type:** CDN provider total failure or complete loss of traffic delivery
**Response SLA:** Declare within 15 minutes · First customer comms within 20 minutes
**Last reviewed:** April 2026

---

## Overview

A CDN total outage occurs when all or nearly all traffic through the CDN layer fails — resulting in 5xx errors, timeouts, or complete inaccessibility for end users. This is the highest-impact infrastructure incident type and requires immediate, coordinated cross-functional response.

This runbook covers Fastly-pattern CDN architecture but the triage logic applies to any edge cloud provider (Cloudflare, Akamai, AWS CloudFront).

**Do not wait for confirmation before declaring P1.** If monitoring shows error rates above 50% across multiple regions, declare immediately and investigate in parallel.

---

## Roles and responsibilities

| Role | Responsibility | Assigned to |
|---|---|---|
| **Incident Commander (IC)** | Owns the response end-to-end. Makes all decisions. | On-call lead |
| **Technical Lead** | Drives triage and diagnosis. Reports findings to IC. | Senior support / infra engineer |
| **Comms Lead** | Drafts and sends all customer and stakeholder communications. | Support engineer or CSM |
| **Scribe** | Documents all actions and timestamps in real time on the incident ticket. | Any available engineer |
| **Executive Sponsor** | Available for escalation. Notified but not in the bridge unless P1 exceeds 60 min. | Engineering VP / Head of Support |

> **IC rule:** The IC does not triage. The IC coordinates, delegates, and communicates. If the IC is also debugging, they are not doing their job.

---

## Detection signals

You are likely dealing with a CDN total outage if **two or more** of the following are true:

- [ ] Synthetic monitoring shows >50% failure rate across 3+ probe locations
- [ ] Customer-reported errors spiking in support queue (multiple companies, not one)
- [ ] CDN provider status page shows active incident
- [ ] Internal health checks to CDN edge IPs returning 5xx or timeout
- [ ] Error rate in observability dashboard above 40% on CDN-routed endpoints
- [ ] Origin servers healthy (ruling out an origin-side incident)

---

## Step-by-step response

### Phase 1 — Declare and mobilise (0–10 minutes)

- [ ] **Declare P1.** Post in `#incidents`:

  ```
  [P1 DECLARED] CDN possible total outage — [timestamp UTC]
  IC: @[your name]
  Bridge: [Zoom/Meet link]
  Ticket: [link]
  ```

- [ ] **Open the incident ticket.** Title format: `P1 - CDN Total Outage - [YYYY-MM-DD HH:MM UTC]`
- [ ] **Start the bridge call.** IC opens it; do not wait for everyone before starting triage.
- [ ] **Assign roles** from the table above. Name each person on the bridge and in the ticket.
- [ ] **Notify the Executive Sponsor** via DM: *"P1 declared, CDN suspected outage, we are in bridge, will update in 15."*
- [ ] **Tag the incident ticket** with: `p1`, `cdn`, `in-progress`

---

### Phase 2 — Triage and diagnosis (10–25 minutes)

The Technical Lead drives this phase. The IC listens, manages the bridge, and ensures the Scribe is documenting.

#### 2a — Confirm CDN failure vs origin failure

```bash
# Test direct origin (bypassing CDN) — replace with your origin IP
curl -I https://your-origin-ip.example.com/health \
  -H "Host: www.yoursite.com" \
  --resolve www.yoursite.com:443:YOUR_ORIGIN_IP

# 200 response = origin healthy = CDN is the problem → continue this runbook
# Failure       = origin also down = open origin outage runbook instead
```

- [ ] Origin **healthy** → confirmed CDN-side failure, continue
- [ ] Origin **also failing** → stop, open origin outage runbook

#### 2b — Identify scope

```bash
# Check CDN edge health across regions
for region in fra lax sjc iad nrt syd; do
  echo "=== $region ==="
  curl -sI --max-time 10 https://www.yoursite.com \
    2>&1 | grep -E "HTTP|curl|connect"
done
```

Determine:
- [ ] All regions or specific PoPs?
- [ ] All services or specific domains / paths?
- [ ] All customers or a subset?

#### 2c — Check CDN provider status

- [ ] Open CDN provider status page (bookmark — do not search during an incident)
  - Fastly: https://www.fastlystatus.com
  - Cloudflare: https://www.cloudflarestatus.com
- [ ] Check provider Twitter/X account for customer reports
- [ ] **Call the enterprise support line** — do not rely on the status page alone for P1s

#### 2d — Review recent changes

- [ ] Config deploy to CDN in the last 2 hours?
- [ ] DNS change in the last 24 hours?
- [ ] TLS certificate renewal recently?
- [ ] Firewall rules or WAF policies updated?

If a change is identified: this is likely the cause. Move to Phase 3b (rollback).

---

### Phase 3a — Mitigation: CDN provider incident

- [ ] **Activate origin failover** if configured — route traffic directly to origin
  - Document the command in the ticket and get IC approval before executing
- [ ] **Update DNS** to point directly to origin if no failover automation exists
- [ ] **Communicate to customers** — use [p1-initial-notification](../../comms/customer-facing/p1-initial-notification.md)
- [ ] **Stay on the provider support call** until root cause and ETA confirmed
- [ ] **Update the bridge every 15 minutes** — even if the update is "no change"

---

### Phase 3b — Mitigation: Change-caused outage (rollback)

- [ ] Identify the exact change — config version, deploy ID, or commit hash
- [ ] Do not attempt to fix forward unless rollback is impossible
- [ ] **Execute rollback** — document in ticket, IC approves, Technical Lead executes

  ```bash
  # Fastly example — activate previous version
  fastly service-version activate \
    --version PREVIOUS_VERSION_NUMBER \
    --service-id YOUR_SERVICE_ID
  ```

- [ ] **Verify recovery** — re-run Phase 2b curl checks and confirm 200s across regions

---

### Phase 4 — Resolution and handoff

- [ ] Confirm recovery with Technical Lead across all affected regions
- [ ] Send all-clear to customers — use [p1-all-clear](../../comms/customer-facing/p1-all-clear.md)
- [ ] Send internal all-clear to Executive Sponsor and leadership channel
- [ ] Post Scribe's timeline to the incident ticket
- [ ] Update ticket status to `Resolved`
- [ ] **Schedule RCA within 48 hours** — IC books calendar invite before closing bridge
- [ ] Close the bridge: *"We're closing the bridge. RCA is scheduled for [date/time]. Thanks everyone."*

---

## Escalation path

```
On-call engineer
       ↓ (no response in 5 min)
Senior support engineer / IR lead
       ↓ (P1 unresolved at 30 min)
Head of Support / Engineering Manager
       ↓ (P1 unresolved at 60 min)
VP Engineering / CTO
       ↓ (customer contract / SLA breach imminent)
Account team + Legal
```

---

## Key metrics to capture

| Metric | Notes |
|---|---|
| **Detection time** | When did monitoring first alert? |
| **Declaration time** | When was P1 formally declared? |
| **Customer impact start** | Earliest confirmed customer-facing error |
| **Bridge open time** | When did the response bridge open? |
| **First customer comms sent** | Timestamp of first external communication |
| **Mitigation applied** | What was done, by whom, at what time? |
| **Recovery confirmed** | When did error rates return to baseline? |
| **All-clear sent** | Timestamp of external resolution notice |
| **Total duration** | Customer impact start → recovery confirmed |

---

## Common false positives

Do not declare P1 for:
- A single customer reporting issues (check if others are affected first)
- A single probe location failing (check multiple regions)
- Elevated latency without elevated error rates
- A CDN provider posting a minor status page incident with no customer-confirmed impact

---

## Related documents

- [Escalation matrix](../../escalation/escalation-matrix.md)
- [P1 initial customer notification](../../comms/customer-facing/p1-initial-notification.md)
- [P1 all-clear notification](../../comms/customer-facing/p1-all-clear.md)
- [Internal bridge update template](../../comms/internal/bridge-update.md)
- [Blameless RCA template](../../rca/blameless-rca-template.md)

---

*Runbook owner: IR Lead · Review cycle: Quarterly · Last reviewed: April 2026*
