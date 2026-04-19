# Customer comms: P1 initial notification

**Use:** Within 20 minutes of declaring P1 — before you have a root cause.
**Channels:** Status page · Email to affected accounts · In-app banner (if available)
**Tone:** Clear, factual, calm. No speculation. No apologies that imply fault before investigation.

---

## Status page update

**Title:**
```
Investigating: Service disruption affecting [product/service name]
```

**Body:**
```
We are currently investigating reports of [brief description — e.g. "errors and timeouts
affecting our CDN-delivered services"].

Our team has been alerted and is actively investigating. We will provide an update
within 30 minutes.

Started: [HH:MM UTC]
```

---

## Direct email to affected enterprise accounts

**Subject:**
```
[Action required] Service disruption — [Your Company] — [HH:MM UTC]
```

**Body:**
```
Hi [First name / Team],

We want to make you aware of a service disruption we are currently investigating.

What is affected: [One sentence]
Who is affected: [All customers / Customers in the EU region / etc.]
Current status: Our incident response team declared this a P1 at [HH:MM UTC] and is
actively investigating. We do not yet have a root cause.

What you can do: [Workaround if available, or "No action is required from your side."]

Next update: We will send a follow-up within 30 minutes, or sooner if we have new information.

We apologise for the disruption and will keep you informed throughout.

[Your name]
[Title] · [Company]
Incident reference: [INC-XXXXX]
```

---

## Notes on tone

- Do **not** say "we apologise for any inconvenience" — dismissive during a real outage.
- Do **not** speculate on cause.
- Do **not** promise a fix time unless the Technical Lead has confirmed it.
- **Do** use precise UTC timestamps.
- **Do** give a concrete next-update time and honour it.
