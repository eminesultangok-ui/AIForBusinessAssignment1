# P10 · Event closure / reconciliation

**Section:** 03 — Compliance & Reporting


**Workflow step:** Step 4 of 4


**Current version:** v1.0


**Status:** ✅ Tested and approved


**Last updated:** August 2026

---

## 📌 Prompt Text (v1.0 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions operations analyst at an investment
banking company. Summarise this closed corporate action event for
internal records: total clients notified, instructions received vs
lapsed, any exceptions requiring follow-up. Max 150 words.

Before drafting, check that the event closure data field has real
values (not placeholders or blank). If missing, output only: "Missing
required data: event closure data."

Do not add an analyst name — sign the document only as "Corporate
Actions Operations." Do not invent missing data, and do not add
fields outside this list.


```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[Event Closure Data]` | Corporate actions system | Event Name: DEF Holdings — Merger. Total Clients Notified: 45. Instructions Received (Participated): 38. Lapsed (No Instruction Received): 5. Exceptions Requiring Follow-up: 2 (missing exchange ratio data for 2 accounts). |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 4** of the Compliance and Reporting stage — the final step in the corporate actions chain, where all paths converge.

- **Trigger:** All client instructions processed / event reaches its closure date
- **Actor:** Corporate actions analyst
- **Timing:** On event closure date
- **Next step:** Process ends; record archived for audit

```
All instructions processed / closure date reached --> P10 runs --> Archived for audit
```

---

## ❗ Problem Being Solved

Closure records are currently inconsistent, and sometimes not kept at all — this creates gaps in the audit trail.

**Pain points addressed:**
- No standardised closure record across analysts
- Audit trail gaps when closure summaries are skipped
- Difficulty reconstructing "what happened" on a past event without a formal record

---

## ⚡ Automation Potential

**Level: High**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | High — every event needs one |
| Data availability | Full event record available at closure |
| Human judgment needed | Low |
| Integration possibility | Could trigger automatically at closure date |
| Estimated time saving | ~80% |

**Human-in-the-loop role:** Analyst confirms figures reconcile with the system before archiving.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| Figures don't reconcile with system | Medium | Analyst verification before archiving — record is used for audit purposes |

**Overall risk rating: LOW**

---

## 🔄 Version History

### v1.0 — Initial draft ✅ Current

**Date:** 11 August 2026


**Prompt:** `Summarise this closed corporate action event for internal records: total clients notified, instructions received vs lapsed, any exceptions requiring follow-up. Max 150 words. Do not invent missing data, and do not add fields outside this list.`


**Output:** Accurate closure summary — all figures (45 notified, 38 participated, 5 lapsed, 2 exceptions) reproduced exactly from input, with the exception reason correctly stated.


**Observed effect:** Produces a clean, audit-ready closure record with no invented or altered figures — matches the discipline enforced in P01 (do not invent missing data) applied here to a summary/reporting context.


**Lesson learned:** Constraints proven effective in earlier prompts (explicit field list, no invented data) transferred cleanly to a new context (event closure) without needing further iteration — confirming these are now reliable, reusable prompt-design patterns across the library.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score |
|----------|------------|
| Figure accuracy | 5.0/5 |
| No invented data | 5.0/5 |
| Audit-record tone | 4.8/5 |
| Constraint compliance | 5.0/5 |
| **Overall** | **4.95/5** |

---

## 🔗 Related Prompts

- **Previous in chain:** [P05 — Instruction confirmation](P05-instruction-confirmation.md), [P07 — Missed deadline](P07-missed-deadline.md), [P09 — Complex event FAQ](P09-complex-event-faq.md)
- **Parent section:** [03-compliance-and-reporting](../workflows/03-compliance-and-reporting/README.md)
