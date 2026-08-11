# P08 · Daily processing digest

**Section:** 03 — Compliance & Reporting
**Workflow step:** Step 2 of 4
**Current version:** v1.0
**Status:** ✅ Tested and approved
**Last updated:** August 2026

---

## 📌 Prompt Text (v1.0 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions operations lead at an investment banking
company. Summarise today's processed corporate action events for
internal management reporting — this is not a client-facing
communication.

Using this daily processing log, extract each event and present it
as a table with columns: Company, Event Type, Status, Client Count
Affected. Flag any row with Status "Exception" for escalation,
listing the exception reason if provided.

Before drafting, check that the daily processing log field has real
values (not placeholders or blank). If missing, output only: "Missing
required data: daily processing log."

Do not add an analyst name — sign the report only as "Corporate
Actions Operations."

Daily Processing Log:
[Daily Processing Log]
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[Daily Processing Log]` | Daily Processing Log | 1. AAPL — Dividend — Completed — 100 clients affected. 2. ABC Ltd — Rights Issue — Completed — 80 clients affected. 3. DEF Holdings — Merger — Exception (missing exchange ratio data) — 45 clients affected. 4. GHI Group — Stock Split — Completed — 890 clients affected. 5. JKL Industries — Tender Offer — Pending — 15 clients affected. |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 2** of the Compliance and Reporting stage. Runs in parallel to individual events — independent of any single corporate action.

- **Trigger:** Every morning, once the previous day's events are fully processed
- **Actor:** Corporate actions operations lead
- **Timing:** Before the morning ops stand-up
- **Next step:** Exception rows investigated manually

```
Daily processing complete --> P08 runs each morning --> Ops lead reviews
                                                       --> Exceptions investigated
```

---

## ❗ Problem Being Solved

The ops lead manually compiles this status overview from multiple systems each morning, ~30 minutes.

**Pain points addressed:**
- Manual compilation from multiple systems is time-consuming
- Exception rows can be missed or buried in a long unformatted log
- No standardised format across different days/analysts

---

## ⚡ Automation Potential

**Level: High**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | Daily, every business day |
| Data availability | Full log available from processing system |
| Human judgment needed | Low — exceptions still need manual investigation |
| Integration possibility | Could be scheduled to auto-generate each morning |
| Estimated time saving | ~90% |

**Human-in-the-loop role:** Ops lead investigates flagged exception rows; digest itself needs no sign-off before internal use.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| Depends entirely on source log accuracy | Medium | Log accuracy is a separate, existing control; not introduced by this prompt |
| Exceptions flagged but not resolved | Low | Digest only flags — resolution remains a manual, tracked process |

**Overall risk rating: LOW**

---

## 🔄 Version History

### v1.0 — Initial draft ✅ Current

**Date:** 11 August 2026
**Prompt:** `Summarise today's processed corporate action events for internal management reporting. Extract each event and present as a table: Company, Event Type, Status, Client Count Affected. Flag any Exception rows for escalation.`
**Output:** Correct 4-column table with all 5 events accurately extracted; added a relevant "Exception Reason" column and an escalation note for the flagged event.
**Observed effect:** Ops lead gets an immediately scannable table plus a clear escalation flag — no manual sorting or interpretation needed.
**Lesson learned:** Separating P08's internal-reporting role from P07's client-facing role (which had been mistakenly mixed into the first draft) was essential — once the prompt focused solely on tabular extraction and escalation flagging, the model produced a clean, accurate result on the first well-scoped attempt.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score |
|----------|------------|
| Data extraction accuracy | 5.0/5 |
| Table formatting | 5.0/5 |
| Exception flagging | 5.0/5 |
| Report tone (internal, not client-facing) | 5.0/5 |
| **Overall** | **5.0/5** |

---

## 🔗 Related Prompts

- **Parent section:** [03-compliance-and-reporting](../workflows/03-compliance-and-reporting/README.md)
- Runs in parallel to all other prompts in this chain
