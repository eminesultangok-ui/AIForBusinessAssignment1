[README.md](https://github.com/user-attachments/files/30920887/README.md)
# 📂 02 — Deadline and Instruction Management

**Business function:** Corporate Actions Operations
**Trigger:** A Voluntary event notification (P03) has been sent
**Prompts in this section:** P04, P05, P07

---

## Section Purpose

These prompts manage the client decision window for Voluntary events (rights issues, tender offers). They never run on the Mandatory path, since mandatory events require no client decision.

## Chain Diagram

```
P03 sent (Voluntary notification)
    |
    v
P04 - Deadline reminder
    |
    +-- Instructed --> P05 - Instruction confirmation
    |
    +-- Deadline missed --> P07 - Missed-deadline follow-up
```

## Human-in-the-Loop Points

| Step | Human action required |
|------|------------------------|
| P04 output | Minimal — scheduling/trigger check only |
| P05 output | Analyst spot-checks reference number matches system record |
| P07 output | Analyst reviews tone before sending — mandatory, given client sensitivity |

## Prompts

| File | Prompt | Status |
|------|--------|--------|
| [P04-deadline-reminder.md](../../prompts/P04-deadline-reminder.md) | Deadline reminder | ✅ Tested — v1.1 |
| [P05-instruction-confirmation.md](../../prompts/P05-instruction-confirmation.md) | Instruction confirmation | ✅ Tested — v1.1 |
| [P07-missed-deadline.md](../../prompts/P07-missed-deadline.md) | Missed-deadline follow-up | ✅ Tested — v1.0 |
