# Customer comms: P1 all-clear

**Use:** Once recovery is confirmed by the Technical Lead — do not send until confirmed.
**Channels:** Status page · Email to affected accounts
**Tone:** Direct and confident. Acknowledge impact honestly. Signal follow-up.

---

## Status page update

**Title:**
```
Resolved: Service disruption affecting [product/service name]
```

**Body:**
```
This incident has been resolved. Services are operating normally as of [HH:MM UTC].

Impact summary: [e.g. "Customers experienced errors on CDN-delivered requests between
HH:MM and HH:MM UTC — approximately X minutes of disruption."]

We will publish a post-incident summary within 48 hours.

Resolved: [HH:MM UTC]
Duration: [X hours Y minutes]
```

---

## Direct email to affected enterprise accounts

**Subject:**
```
Resolved: Service disruption — [Your Company] — [HH:MM UTC]
```

**Body:**
```
Hi [First name / Team],

We can confirm that the service disruption affecting [product/service name] has been
resolved as of [HH:MM UTC].

Impact: [Honest summary of what failed and for how long.]
Duration: Approximately [X] minutes.

What we did: [One or two sentences on the mitigation — e.g. "We identified a
misconfiguration in our CDN routing layer and rolled back to the previous stable
configuration."]

Next steps: Our team will conduct a full post-incident review within 48 hours and
share a summary including root cause and steps to prevent recurrence.

[Your name]
[Title] · [Company]
Incident reference: [INC-XXXXX]
```

---

## Notes on tone

- **Name the duration honestly.** Customers already know how long it lasted.
- **Don't oversell the fix.** Say what you did, not what you'll never let happen again.
- **Commit to the post-incident report.** 48 hours is the standard. Honour it.
- **Enterprise accounts expect a call** if the outage exceeded 30 minutes.
