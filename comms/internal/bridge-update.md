# Internal comms: bridge update template

**Use:** Every 15 minutes during a P1 bridge. Every 30 minutes during a P2.
**Channel:** `#incidents` Slack channel + incident ticket comment
**Posted by:** Scribe (on behalf of IC)

---

## 15-minute bridge update

```
[P1 UPDATE] [HH:MM UTC] — [Incident title]

Status: [Investigating / Mitigating / Monitoring / Resolved]

What we know:
- [Confirmed facts only — no speculation]
- [Bullet]

What we're doing:
- [Current active action and owner]
- [Bullet]

Blockers:
- [Any blockers, or "None"]

Next update: [HH:MM UTC] or sooner if status changes.

IC: @[name] · Tech Lead: @[name] · Ticket: [INC-XXXXX]
```

---

## Executive update (T+30 min if unresolved)

**Send via:** Direct Slack message — not bridge channel
**Length:** 5 lines maximum

```
P1 Update [HH:MM UTC] — [Incident title]

Declared: [HH:MM UTC] | Duration so far: [X min]
Customer impact: [One sentence]
Current action: [What Technical Lead is doing right now]
ETA: [Best estimate, or "Unknown — will update at HH:MM"]
```

---

## Bridge closure message

```
[P1 RESOLVED] [HH:MM UTC] — [Incident title]

Services restored at [HH:MM UTC].
Total duration: [X hours Y minutes]

All-clear sent to customers: [Yes/No — timestamp if yes]
RCA scheduled: [Date · Time · Invite sent to: @names]

Thank you to: @[IC], @[Tech Lead], @[Scribe], @[Comms Lead]

Ticket: [INC-XXXXX] — status updated to Resolved.
```
