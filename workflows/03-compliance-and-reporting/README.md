[README.md](https://github.com/user-attachments/files/30920952/README.md)
# 📂 03 — Compliance and Reporting

**Business function:** Corporate Actions Operations / Compliance
**Trigger:** Varies — pre-send screening, daily schedule, or event closure
**Prompts in this section:** P06, P08, P09, P10

---

## Section Purpose

These prompts provide the internal control layer of the workflow: pre-send compliance screening, daily operational reporting, client service preparation for complex events, and final event closure for audit purposes.

## Chain Diagram

```
P02 / P03 draft --> P06 - Compliance check --> sent to client

P01 flags "complex event" --> P09 - Complex event FAQ (for CS team)

All paths converge --> P10 - Event closure / reconciliation

PARALLEL, ALWAYS-ON:
P08 - Daily processing digest -- runs every morning, independent of any single event
```

## Human-in-the-Loop Points

| Step | Human action required |
|------|------------------------|
| P06 output | NOT a compliance sign-off — qualified human reviewer mandatory for every email |
| P08 output | Ops lead investigates any flagged exception rows |
| P09 output | Must be compliance-reviewed before use on live client calls |
| P10 output | Analyst confirms figures reconcile with the system before archiving |

## Prompts

| File | Prompt | Status |
|------|--------|--------|
| [P06-compliance-check.md](../../prompts/P06-compliance-check.md) | Pre-send compliance screening | ✅ Tested — v1.0 |
| [P08-daily-digest.md](../../prompts/P08-daily-digest.md) | Daily processing digest | ✅ Tested — v1.0 |
| [P09-complex-event-faq.md](../../prompts/P09-complex-event-faq.md) | Complex event FAQ prep | ✅ Tested — v1.1 |
| [P10-event-closure.md](../../prompts/P10-event-closure.md) | Event closure / reconciliation | ✅ Tested — v1.0 |
