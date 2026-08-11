# P04 · Deadline reminder

**Section:** 02 — Deadline and Instruction Management

**Workflow step:** Step 1 of 3

**Current version:** v1.1

**Status:** ✅ Tested and approved

**Last updated:** August 2026

---

## 📌 Prompt Text (v1.1 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions analyst at an investment banking company.
This is a follow-up reminder — the client has not yet responded to a
voluntary corporate action notification sent previously.

Using this event data — Security Name, ISIN, holding shares amount,
deadline for instruction — write a 90-word reminder email in plain
language, sent on behalf of the bank named below. Do not re-explain
the full event terms in detail; briefly reference that full details
were sent in the original notification.

Bold the deadline. Clearly state that if no instruction is submitted
by the deadline, the client's rights under this event will lapse. End
with a specific call to action: ask the client to submit their
instruction (participate or decline) and state how to do so (e.g. via
their relationship manager).

Before drafting, check that all required fields have real values (not
placeholders or blanks). If any required field is missing, output
only: "Missing required data: [field name]."

Do not add an analyst name — sign the notification only as
"Corporate Actions Team." Do not recommend whether the client should
participate.

Event feed entry:
Sender Name: [Sender Name]
Security Name: [Security Name]
ISIN: [ISIN]
Holding Shares Amount: [Holding Shares Amount]
Deadline Date: [DEADLINE_DATE]
Event Terms: [EVENT TERMS]
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

This prompt is **Step 1** of the Deadline and Instruction Management stage (Voluntary path only).

- **Trigger:** X days after P03 is sent, if no instruction is on record
- **Actor:** Corporate actions analyst (reviews and sends output)
- **Timing:** Configurable lead time before deadline (e.g. 5 days prior)
- **Next step:** Instruction arrives → P05. Deadline passes → P07.

```
P03 sent --> no instruction after X days --> P04 runs --> Instructed: P05
                                                          --> Missed: P07
```

---

## ❗ Problem Being Solved

Missed voluntary-action deadlines are a recurring client complaint source; reminders are currently sent late, inconsistently, or duplicate the full original notification instead of serving as a brief follow-up.

**Pain points addressed:**
- Reminders sometimes forgotten or sent late
- Risk of reminders duplicating P03 instead of being brief and urgency-focused
- Inconsistent deadline emphasis across analysts

---

## ⚡ Automation Potential

**Level: High**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | High |
| Data availability | Deadline in calendar, instruction status in system |
| Human judgment needed | Low |
| Integration possibility | Could trigger automatically from the calendar |
| Estimated time saving | ~75% |

**Human-in-the-loop role:** Minimal — mainly a scheduling/trigger check.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| Reminder duplicates full P03 notification | Medium (resolved in v1.1) | Explicit "reference, don't repeat" instruction added |
| Deadline not visually emphasised | Low (resolved in v1.1) | Bold formatting now required |
| Implies a recommendation | Low | Prompt explicitly avoids advising |

**Overall risk rating: LOW**

---

## 🔄 Version History

### v1.0 — Initial draft

**Date:** 11 August 2026


**Prompt:** `Write a reminder email for a voluntary event, asking for instruction, warning that rights will lapse if no response.`


**Output:** Accurate and complete — correctly included the rights-lapse warning, terms, and call to action. However, the notification re-explained the full event terms in detail, almost identically to what P03 would have already sent, and the deadline was not visually emphasised (no bold formatting requested).


**Observed effect:** The output functioned as a strong standalone notification, but not as a distinct "reminder" — it largely duplicated P03's content rather than serving its intended role of a brief, urgency-focused follow-up.


**Lesson learned:** A reminder prompt needs to be explicitly instructed to be brief and to reference (not repeat) previously sent details, or the model defaults to producing a full notification again — the workflow's distinction between P03 (full notification) and P04 (reminder) needs to be enforced in the prompt, not assumed.

---

### v1.1 — Shortened to a true reminder, referencing rather than repeating terms ✅ Current

**Date:** 11 August 2026


**Change:** Reduced word limit to 90 words; instructed model to reference (not repeat) event terms; required bolded deadline; framed as a reminder, not a first notification.


**Output:** Shorter, urgency-focused reminder that referenced the original notification instead of restating terms, with the deadline bolded.


**Observed effect:** P04 now reads as a genuine reminder rather than duplicating P03 — a clear, distinct role within the workflow.


**Lesson learned:** The model defaults to a full notification unless told it's a follow-up — framing and structural instructions (reference, don't repeat; bold the deadline) were both necessary.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score | v1.1 score |
|----------|------------|------------|
| Distinctness from P03 | 2.0/5 | 4.7/5 |
| Deadline emphasis | 2.0/5 | 5.0/5 |
| Conciseness | 2.5/5 | 4.6/5 |
| Constraint compliance | 5.0/5 | 5.0/5 |
| **Overall** | **2.9/5** | **4.8/5** |

---

## 🔗 Related Prompts

- **Previous in chain:** [P03 — Voluntary notification](P03-voluntary-notification.md)
- **Next in chain:** [P05 — Instruction confirmation](P05-instruction-confirmation.md) or [P07 — Missed deadline](P07-missed-deadline.md)
- **Parent section:** [02-deadline-and-instruction-management](../workflows/02-deadline-and-instruction-management/README.md)
