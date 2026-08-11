[README.md](https://github.com/user-attachments/files/30920823/README.md)
# 📂 01 — Event Classification and Notification

**Business function:** Corporate Actions Operations
**Trigger:** Custodian data feed delivers a new corporate action record
**Prompts in this section:** P01, P02, P03

---

## Section Purpose

These prompts handle the first stage of every corporate action event: determining whether it is Mandatory or Voluntary, and drafting the appropriate client notification. This is the highest-volume stage, covering all ~150 monthly events.

## Chain Diagram

```
Custodian data feed
    |
    v
P01 - Classify event (Mandatory or Voluntary?)
    |
    +-- Mandatory --> P02 - Client notification
    |
    +-- Voluntary --> P03 - Notification + instruction request
```

## Human-in-the-Loop Points

| Step | Human action required |
|------|------------------------|
| P01 output | Analyst confirms classification, checks field status (Present/Missing/Ambiguous/Not Applicable) |
| P02 / P03 output | Analyst dual-checks dates/rates/terms against custodian feed before send |

## Prompts

| File | Prompt | Status |
|------|--------|--------|
| [P01-event-classification.md](../../prompts/P01-event-classification.md) | Event classification | ✅ Tested — v1.4 |
| [P02-mandatory-notification.md](../../prompts/P02-mandatory-notification.md) | Mandatory event notification | ✅ Tested — v1.1 |
| [P03-voluntary-notification.md](../../prompts/P03-voluntary-notification.md) | Voluntary event notification | ✅ Tested — v1.1 |
