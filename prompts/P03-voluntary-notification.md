# P03 · Voluntary event notification

**Section:** 01 — Event Classification & Notification

**Workflow step:** Step 3 of 3


**Current version:** v1.1

**Status:** ✅ Tested and approved

**Last updated:** August 2026

---

## 📌 Prompt Text (v1.1 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions analyst at an investment banking company.
This event has already been classified as Voluntary by the upstream
classification step.

Using this event data — Security Name, ISIN, holding shares amount,
event terms, deadline for instruction — write a 120-word client
notification in plain language, sent on behalf of the bank named
below.

Clearly explain what the client is being asked to decide, using the
event terms provided. End with a specific call to action: ask the
client to submit their instruction (participate or decline) before
the stated deadline, and state how to do so (e.g. via their
relationship manager).

Before drafting, check that all required fields listed above have
real values (not placeholders or blanks). If any required field is
missing or clearly a placeholder, do not draft the notification —
instead output only: "Missing required data: [field name]."

Do not add an analyst name — sign the notification only as
"Corporate Actions Team." Do not recommend whether the client should
participate.


```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[Sender Name]` | Sender Name | BLUE INVESTMENT BANKING COMPANY |
| `[Security Name]` | Security Name | AAPL-APPLE |
| `[ISIN]` | Corporate action notice / security details | US0378331005 |
| `[Holding Shares Amount]` | Security Holding Amount | 100 |
| `[DEADLINE_DATE]` | Corporate action deadline dates | 20.08.2026 |
| `[EVENT TERMS]` | Corporate action terms | Rights issue — eligible for 1 new share for every 3 shares held, at a subscription price of USD 15.00 per new share |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 2** of the corporate actions processing chain (Voluntary path).

- **Trigger:** P01 classifies the event as Voluntary
- **Actor:** Corporate actions analyst (reviews and sends output)
- **Timing:** Same day as classification
- **Next step:** P06 (compliance check)

```
P01 (Voluntary) --> P03 runs --> Analyst reviews --> P06 (compliance check)
```

---

## ❗ Problem Being Solved

Analysts repeatedly draft the same instruction-request structure for every voluntary event, roughly 15 minutes per event, and must remember every time to include full decision context and a clear call to action.

**Pain points addressed:**
- Repetitive drafting for a lower-frequency but higher-stakes event type
- Risk of omitting the actual decision terms, leaving clients unable to decide
- Risk of ending with a vague referral instead of a specific instruction request

---

## ⚡ Automation Potential

**Level: High**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | High |
| Data availability | Terms, holdings, and deadline all exist in the custodian feed |
| Human judgment needed | Low — accuracy check only |
| Integration possibility | Could trigger automatically once P01 classifies |
| Estimated time saving | ~70% |

**Human-in-the-loop role:** Analyst verifies terms and deadline against the authoritative feed before send.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| Numeric terms (ratio, price) altered or misstated | Medium | Tested with deliberately non-default figures — model reproduced them exactly, no alteration observed |
| Wording implies a recommendation | Low | Prompt explicitly excludes recommendation; caught again at P06 |
| Deadline field re-typed incorrectly | Medium | Must be pulled from the authoritative corporate actions calendar, not manually re-typed |

**Overall risk rating: LOW–MEDIUM**

---

## 🔄 Version History

### v1.0 — Initial draft

**Date:** 11 August 2026


**Prompt:** `Write a client notification requesting instruction for a voluntary corporate action.`


**Output:** Well-formatted, correctly excluded analyst name and recommendation language. But the notification never explained what the client was actually being asked to decide (no event terms provided), and ended with a vague referral ("contact your account manager") instead of a specific instruction request.


**Observed effect:** Output looked complete on the surface but didn't fulfil P03's actual role in the workflow — a Voluntary notification is supposed to request an instruction, not just inform. The client would not know what decision to make or how to respond.


**Lesson learned:** A well-formatted, constraint-compliant output can still fail its core purpose if the prompt doesn't require the two things the task actually needs: the decision context (event terms) and an explicit call to action (how to submit an instruction).

---

### v1.1 — Added event terms field and explicit call to action ✅ Current

**Date:** 11 August 2026


**Change:** Added "Event Terms" field for decision context; required an explicit call to action asking the client to submit an instruction and how.


**Output:** Notification clearly stated the subscription ratio (1:3) and price ($15.00), matched input data exactly, and ended with a specific instruction request instead of a vague referral.


**Observed effect:** Both v1.0 gaps closed — client now knows what's being offered and how to respond.


**Lesson learned:** Adding decision context and a clear call to action turned a well-formatted but functionally incomplete notification into one that actually does its job.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score | v1.1 score |
|----------|------------|------------|
| Decision context clarity | 1.5/5 | 4.8/5 |
| Numeric accuracy | 4.5/5 | 4.9/5 |
| Call to action clarity | 2.0/5 | 4.7/5 |
| Constraint compliance (no recommendation, no analyst name) | 5.0/5 | 5.0/5 |
| **Overall** | **3.3/5** | **4.9/5** |

---

## 🔗 Related Prompts

- **Previous in chain:** [P01 — Event classification](P01-event-classification.md)
- **Next in chain:** [P06 — Compliance check](P06-compliance-check.md)
- **Parent section:** [01-event-classification-and-notification](../workflows/01-event-classification-and-notification/README.md)
