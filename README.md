# 📚 Prompt Library — Investment Banking Operations: Corporate Actions Processing

> **Assessment 1 | Generative AI for Business**
> Student: Emine Sultan Gok | Business Field: Investment Banking Operations — Corporate Actions Processing
> Model tested on: OpenAI GPT-4.1 Mini (via La Trobe Prompt Lab)
> Last updated: 11 August 2026

---

## What This Library Does

This prompt library supports the end-to-end automation of **corporate actions processing** at a mid-sized investment bank (Solstice Capital Markets, fictional). It contains **10 documented, tested, and iterated prompts** organised into three workflow stages that together trace a single corporate action event — dividend, stock split, merger, or rights issue — from raw data classification through client notification, compliance screening, and closure/reconciliation.

Each prompt entry follows the same structure:
- The exact prompt text (with placeholders)
- The workflow task it supports
- The problem it solves
- Its automation potential
- Known risks and mitigations
- Version history and test results

---

## 📂 Folder Structure

```
AIForBusinessAssignment1/
│
├── README.md                                              ← You are here (library index)
│
├── workflows/
│   ├── 01-event-classification-and-notification/README.md
│   ├── 02-deadline-and-instruction-management/README.md
│   └── 03-compliance-and-reporting/README.md
│
└── prompts/
    ├── P01-event-classification.md
    ├── P02-mandatory-notification.md
    ├── P03-voluntary-notification.md
    ├── P04-deadline-reminder.md
    ├── P05-instruction-confirmation.md
    ├── P06-compliance-check.md
    ├── P07-missed-deadline.md
    ├── P08-daily-digest.md
    ├── P09-complex-event-faq.md
    └── P10-event-closure.md
```

---

## 📊 Library Summary Table

| ID | Prompt Name | Workflow | Automation Level | Risk Level | Status |
|----|-------------|----------|-------------------|------------|--------|
| P01 | Event classification | Event Classification & Notification | High | Low–Medium | ✅ Tested — v1.4 |
| P02 | Mandatory notification | Event Classification & Notification | High | Low–Medium | ✅ Tested — v1.1 |
| P03 | Voluntary notification | Event Classification & Notification | High | Low–Medium | ✅ Tested — v1.1 |
| P04 | Deadline reminder | Deadline & Instruction Management | High | Low | ✅ Tested — v1.1 |
| P05 | Instruction confirmation | Deadline & Instruction Management | High | Low | ✅ Tested — v1.1 |
| P06 | Compliance check | Compliance & Reporting | High | Medium | ✅ Tested — v1.0 |
| P07 | Missed-deadline follow-up | Deadline & Instruction Management | Medium | Medium | ✅ Tested — v1.0 |
| P08 | Daily digest | Compliance & Reporting | High | Low | ✅ Tested — v1.0 |
| P09 | Complex event FAQ | Compliance & Reporting | Medium | Medium | ✅ Tested — v1.1 |
| P10 | Event closure | Compliance & Reporting | High | Low | ✅ Tested — v1.0 |

**Automation levels:** Very High / High / Medium / Low
**Risk levels:** High (always needs human review) / Medium (spot-check recommended) / Low (can automate with audit)

---

## 🔗 Prompt Chaining Map

```
EVENT CLASSIFICATION & NOTIFICATION
P01 (Classify) ──┬── Mandatory ──> P02 (Notify) ─────────┐
                 └── Voluntary ──> P03 (Notify+Request) ─┤
                                                          ▼
                                              P06 (Compliance check)

DEADLINE & INSTRUCTION MANAGEMENT (Voluntary path only)
P04 (Reminder) ──┬── Instructed ──> P05 (Confirm)
                 └── Missed ──────> P07 (Follow-up)

COMPLIANCE & REPORTING
P06 (Compliance) → sent to client
P08 (Daily digest) — parallel, runs every morning
P09 (Complex event FAQ) — triggered when P01 flags a complex event (e.g. merger)
P10 (Event closure) — final step, all paths converge here
```

---

## ⚙️ Prompting Strategies Used

| Strategy | Prompts | Why chosen |
|----------|---------|------------|
| Role-based prompting | P01, P02, P03, P06 | Consistent professional tone matching a corporate actions officer/compliance reviewer |
| Explicit output constraints (word limits, scope exclusions, closed field lists) | P02, P03, P04, P05, P07, P09, P10 | Keeps outputs auditable and reduces compliance risk in a regulated context |
| Self-flagging / scope-limitation instructions | P01, P06 | Model distinguishes factual/present data from ambiguous, missing, or advice-adjacent content it should flag rather than invent or generate |
| Structured/tabular output | P08, P10 | Consistency with internal reporting and audit-record systems matters more than natural prose |

---

## 📝 Iteration Evidence

All prompt versions are documented in each prompt's own file, with dated version history and self-tested A/B scores.

| Prompt | Versions | Key improvement |
|--------|----------|------------------|
| P01 | v1.0 → v1.4 | Progressively fixed unscoped checklist output, silently discarded ambiguous data, and inconsistent handling of non-applicable fields — final version enforces a closed four-state field status (Present/Missing/Ambiguous/Not Applicable) |
| P02 | v1.0 → v1.1 | Separated sender identity from event data; added explicit "no action required" statement for Mandatory events |
| P03 | v1.0 → v1.1 | Added missing decision context (event terms) and a specific call to action, after v1.0 produced a notification that never told the client what they were being asked to decide |
| P04 | v1.0 → v1.1 | Reframed from a full repeated notification into a true, concise reminder that references (not repeats) prior details |
| P05 | v1.0 → v1.1 | Replaced abstract "processed ahead of timeline" language with concrete confirmation that the instruction is automatically reflected in the client's account |
| P09 | v1.0 → v1.1 | Removed a leftover instruction copied from P08 that caused the model to fabricate an entirely invented processing-log table alongside the correct FAQ output |

---

## 📖 References

- Anthropic (2025). *Prompt Engineering Overview.* docs.claude.ai
- Australian Securities Exchange (ASX). *Corporate Actions Processing Standards.*
- Australian Prudential Regulation Authority (2019). *Prudential Standard CPS 234 — Information Security.*
- MIT Sloan (2025). *Prompt Engineering is So 2024 — Try These Prompt Templates Instead.*
- Microsoft (2025). *Get Started with Prompt Library — Copilot Studio.*
