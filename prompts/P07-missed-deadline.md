# P07 · Missed-deadline follow-up

**Section:** 02 — Deadline and Instruction Management

**Workflow step:** Step 3 of 3

**Current version:** v1.0

**Status:** ✅ Tested and approved

**Last updated:** August 2026

---

## 📌 Prompt Text (v1.0 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions analyst at an investment banking company.
This is a notification informing a client that the deadline for a
voluntary corporate action has passed without a valid instruction
being received.

Using this event data — Security Name, ISIN, holding shares amount,
Event Name, deadline date, default outcome — write a 100-word
notification email in plain language, sent on behalf of the bank
named below.

Draft a clear, non-judgemental message explaining: (1) the deadline
has passed, (2) what happens as a result (the stated default
outcome), and (3) that the client can contact their relationship
manager with any questions.

Before drafting, check that all required fields have real values (not
placeholders or blanks). If any required field is missing, output
only: "Missing required data: [field name]."

Do not add an analyst name — sign the notification only as
"Corporate Actions Team."

Event feed entry:
Sender Name: [Sender Name]
Security Name: [Security Name]
ISIN: [ISIN]
Holding Shares Amount: [Holding Shares Amount]
Event Name: [Event Name]
Deadline Date: [Deadline Date]
Default Outcome: [Default Outcome]
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[Sender Name]` | Sender Name | BLUE INVESTMENT BANKING COMPANY |
| `[Security Name]` | Security Name | AAPL-APPLE |
| `[ISIN]` | Corporate action notice / security details | US0378331005 |
| `[Holding Shares Amount]` | Security Holding Amount | 100 |
| `[Event Name]` | Corporate action name | Rights distribution |
| `[Deadline Date]` | Corporate action date | 20.08.2026 |
| `[Default Outcome]` | Corporate action default outcome | Unexercised rights will lapse and no new shares will be allocated |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 3** of the Deadline and Instruction Management stage (Voluntary path only).

- **Trigger:** Deadline passes with no client instruction on record, despite the P04 reminder
- **Actor:** Corporate actions analyst (reviews and sends output)
- **Timing:** Same day the deadline passes
- **Next step:** P10 (event closure)

```
P04 reminder sent --> deadline passes, no instruction --> P07 runs --> P10 (closure)
```

---

## ❗ Problem Being Solved

These emails are sensitive (the client may be upset) and currently vary widely in tone and clarity between analysts, with risk of an unclear or vague default outcome.

**Pain points addressed:**
- Inconsistent tone on a sensitive, client-impacting message
- Risk of vague or generic outcome language instead of a precise stated result
- Client confusion about who to contact for follow-up

---

## ⚡ Automation Potential

**Level: Medium**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | Medium — lower volume than notifications |
| Data availability | Default outcome defined in event terms |
| Human judgment needed | Medium — tone sensitivity |
| Integration possibility | Could trigger automatically, but review recommended |
| Estimated time saving | ~50% (tone still benefits from review) |

**Human-in-the-loop role:** Analyst reviews tone before sending given client sensitivity — non-negotiable for this prompt specifically.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| Wrong tone damages client relationship | Medium | Analyst review before send is mandatory, no exceptions |
| Default outcome stated incorrectly | Low | Sourced from official event terms as an explicit required field, not inferred |
| Ambiguity between "no response" and "late response" scenarios | Low | Prompt scoped to a single, clear scenario: deadline passed, no valid instruction received |

**Overall risk rating: MEDIUM** — low automation confidence due to client-relationship sensitivity, despite low technical risk.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score |
|----------|------------|
| Outcome clarity | 5.0/5 |
| Tone appropriateness | 4.8/5 |
| Contact guidance clarity | 5.0/5 |
| Constraint compliance | 5.0/5 |
| **Overall** | **4.95/5** |

---

## 🔄 Version History

### v1.0 — Initial draft ✅ Current

**Date:** 11 August 2026
**Prompt:** `This is a notification informing a client that the deadline for a voluntary corporate action has passed... Draft a clear, non-judgemental message explaining: (1) the deadline has passed, (2) the default outcome, (3) contact via relationship manager.`
**Output:** Clear, accurate notification — deadline, event name, holding amount, and default outcome all correctly stated; tone was firm but non-judgemental as required.
**Observed effect:** Client receives an unambiguous explanation of what happened and what to do next, with no vague or uncertain language about the outcome.
**Lesson learned:** Making "default outcome" an explicit required field (rather than leaving the model to infer or generalise it) was essential — this is the same lesson learned across P01 and P04: fields the model must state precisely should never be left implicit.

---

## 🔗 Related Prompts

- **Previous in chain:** [P04 — Deadline reminder](P04-deadline-reminder.md)
- **Next in chain:** [P10 — Event closure](P10-event-closure.md)
- **Parent section:** [02-deadline-and-instruction-management](../workflows/02-deadline-and-instruction-management/README.md)
