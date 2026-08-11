# P05 · Instruction confirmation

**Section:** 02 — Deadline and Instruction Management
**Workflow step:** Step 2 of 3
**Current version:** v1.1
**Status:** ✅ Tested and approved
**Last updated:** August 2026

---

## 📌 Prompt Text (v1.1 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions analyst at an investment banking company.
This is a confirmation email acknowledging receipt of a client's
corporate action instruction.

Using this data — Security Name, ISIN, Event Name, Instruction
wording, Reference number, Timeline — write a 90-word confirmation
email in plain language, sent on behalf of the bank named below.

Clearly confirm: (1) the instruction received, stated exactly as
provided, (2) the reference number, for the client's records, and (3)
that the instruction will be processed and automatically reflected in
the client's account ahead of the stated timeline — no further action
is required from the client at this stage.

Before drafting, check that all required fields have real values (not
placeholders or blanks). If any required field is missing, output
only: "Missing required data: [field name]."

Do not add an analyst name — sign the notification only as
"Corporate Actions Team."

Event feed entry:
Sender Name: [Sender Name]
Security Name: [Security Name]
ISIN: [ISIN]
Event Name: [Event Name]
Instruction Wording: [Instruction Wording]
Reference Number: [Reference number]
Timeline: [Timeline]
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[Sender Name]` | Sender Name | BLUE INVESTMENT BANKING COMPANY |
| `[Security Name]` | Security Name | AAPL-APPLE |
| `[ISIN]` | Corporate action notice / security details | US0378331005 |
| `[Event Name]` | Corporate action name | Rights distribution |
| `[Instruction Wording]` | Details of customer instruction | Accepted, 100 shares |
| `[Reference number]` | Corporate action reference number | AB-987132 |
| `[Timeline]` | Corporate action calendar | Ahead of 20.8.2026 |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 2** of the Deadline and Instruction Management stage (Voluntary path only).

- **Trigger:** Client instruction is logged in the system
- **Actor:** Corporate actions analyst (reviews and sends output)
- **Timing:** Same day the instruction is logged
- **Next step:** P10 (event closure)

```
Client instruction logged --> P05 runs --> Analyst checks Ref# --> P10 (closure)
```

---

## ❗ Problem Being Solved

Clients frequently call to confirm their instruction was received, generating avoidable inbound call volume.

**Pain points addressed:**
- Repetitive confirmation drafting for every logged instruction
- Client uncertainty about what happens after submitting an instruction
- Risk of reusing wording from unrelated prompts (e.g. reminder language) instead of true confirmation framing

---

## ⚡ Automation Potential

**Level: High**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | Very high |
| Data availability | All fields exist once instruction is logged |
| Human judgment needed | Very low |
| Integration possibility | Near-complete automation once logged |
| Estimated time saving | ~85% |

**Human-in-the-loop role:** Spot-check that reference number/wording matches the system record exactly.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| Reference number/wording mismatch vs system record | Medium | Must exactly match the logged record to avoid client disputes later |
| Reused wording from unrelated prompt roles | Low (resolved in v1.1) | Instructions rewritten to match P05's specific confirmation role, not copied from P04 |

**Overall risk rating: LOW**

---

## 🔄 Version History

### v1.0 — Initial draft

**Date:** 11 August 2026
**Prompt:** `This is a confirmation email... Clearly confirm: (1) instruction received, (2) reference number, (3) processed ahead of stated timeline — no further action required.`
**Output:** Accurate confirmation — instruction wording reproduced exactly, reference number included, timeline correctly used. But "processed ahead of the timeline" was abstract, not telling the client concretely what happens to their account.
**Observed effect:** Confirmation was correct but not maximally reassuring — lacked concrete detail about automatic account reflection.
**Lesson learned:** Confirming an instruction was "processed" is accurate but vague — clients likely want explicit confirmation that their account updates automatically, with no further steps needed.

---

### v1.1 — Added concrete "automatically reflected in account" detail ✅ Current

**Date:** 11 August 2026
**Change:** Added explicit instruction to confirm the instruction will be "automatically reflected in the client's account" ahead of the timeline, not just "processed."
**Output:** Confirmation now states instruction will be "processed and automatically reflected in your account ahead of 20.8.2026" — more concrete and reassuring than v1.0.
**Observed effect:** Client now has a clear, tangible picture of what happens next, rather than an abstract "processed" statement.
**Lesson learned:** Small wording additions ("processed" → "automatically reflected in your account") can meaningfully improve client reassurance without changing the prompt's structure or length.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score | v1.1 score |
|----------|------------|------------|
| Instruction accuracy | 5.0/5 | 5.0/5 |
| Reference number clarity | 4.8/5 | 4.8/5 |
| Client reassurance | 3.0/5 | 4.9/5 |
| Constraint compliance | 5.0/5 | 5.0/5 |
| **Overall** | **4.5/5** | **4.9/5** |

---

## 🔗 Related Prompts

- **Previous in chain:** [P04 — Deadline reminder](P04-deadline-reminder.md)
- **Next in chain:** [P10 — Event closure](P10-event-closure.md)
- **Parent section:** [02-deadline-and-instruction-management](../workflows/02-deadline-and-instruction-management/README.md)
