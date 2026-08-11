# P09 · Complex event FAQ

**Section:** 03 — Compliance & Reporting


**Workflow step:** Step 3 of 4


**Current version:** v1.1


**Status:** ✅ Tested and approved


**Last updated:** August 2026

---

## 📌 Prompt Text (v1.1 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions operations analyst at an investment
banking company. This event has been flagged as complex (e.g.
merger, spin-off) and is expected to generate a high volume of
inbound client calls.

Given this merger event data, generate exactly 5 FAQ pairs for the
client service team to use during inbound calls. Use plain English,
no jargon without a one-line explanation.

Before drafting, check that the event data field has real values
(not placeholders or blank). If missing, output only: "Missing
required data: event data."

Do not add an analyst name — sign the document only as "Corporate
Actions Operations."

Event Data:
[Event Data]
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[Event Data]` | Corporate actions system | Event Name: Merger — TechCorp Inc. acquiring DataSystems Ltd. Acquirer: TechCorp Inc. Target: DataSystems Ltd. Exchange Ratio: 0.75 shares of TechCorp for every 1 share of DataSystems held. Cash Component: USD 5.00 per share. Expected Completion Date: 15 October 2026. |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 3** of the Compliance and Reporting stage.

- **Trigger:** P01 flags the event as complex (e.g. merger, spin-off) expected to generate high call volume
- **Actor:** Corporate actions analyst, for use by client service team
- **Timing:** Ahead of the event going live to clients
- **Next step:** P10 (event closure)

```
P01 flags "complex" --> P09 runs --> Compliance review --> CS team uses on live calls --> P10
```

---

## ❗ Problem Being Solved

Client service team is unprepared for the surge of calls following a complex event like a merger or spin-off.

**Pain points addressed:**
- CS agents lack corporate actions expertise for complex events
- Risk of inconsistent or inaccurate answers given to clients on live calls
- No prepared reference material ahead of high call-volume events

---

## ⚡ Automation Potential

**Level: Medium**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | Medium — only complex events trigger this |
| Data availability | Event terms available from corporate actions system |
| Human judgment needed | Medium — requires compliance review before live use |
| Integration possibility | Could trigger automatically when P01 flags complexity |
| Estimated time saving | ~60% on FAQ drafting time |

**Human-in-the-loop role:** Must be reviewed against official event terms before being used on live client calls.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| FAQ used on live calls without review | Medium | Mandatory compliance read-through before distribution to CS team |
| Stray instructions cause fabricated data | Low (resolved in v1.1) | Prompt scoped to a single task; verified no unrelated instructions remain |
| Oversimplifies complex terms | Low | Reviewed against official scheme document before use |

**Overall risk rating: MEDIUM**

---

## 🔄 Version History

### v1.0 — Initial draft

**Date:** 11 August 2026
**Prompt:** `Given this merger event data, generate 5 FAQ pairs... [contained a leftover, unrelated instruction copied from P08: "Using this daily processing log, extract each event and present it as a table..."]`
**Output:** The 5 FAQ pairs were accurate and well-written. However, the model also generated an entirely fabricated "Daily Processing Log" table (client counts, status) that was never part of the input — the leftover P08 instruction caused it to invent data with no source.
**Observed effect:** The core FAQ task worked, but the unrelated instruction produced hallucinated data alongside the correct output — a real risk, since the fabricated table looked plausible and could be mistaken for real processing data.
**Lesson learned:** Leftover instructions from a different prompt don't just get ignored — the model will attempt to satisfy them, inventing data if none is provided. Every prompt needs to be checked for stray instructions that don't belong to its own task, not just for whether its main instruction works.

---

### v1.1 — Removed leftover P08 instruction ✅ Current

**Date:** 11 August 2026
**Change:** Removed the unrelated daily-processing-log instruction mistakenly carried over from P08; prompt now contains only the FAQ generation task.
**Output:** 5 accurate FAQ pairs, no fabricated data, correctly signed — matches the input event data exactly.
**Observed effect:** Hallucinated table from v1.0 is gone entirely; output now contains only what was requested.
**Lesson learned:** Removing the single stray instruction eliminated the hallucination — confirming it was caused by the leftover instruction, not a general model tendency to invent data.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score | v1.1 score |
|----------|------------|------------|
| FAQ accuracy | 4.8/5 | 4.9/5 |
| No fabricated data | 1.0/5 | 5.0/5 |
| Plain-English clarity | 4.7/5 | 4.8/5 |
| Task scope compliance | 2.0/5 | 5.0/5 |
| **Overall** | **3.1/5** | **4.9/5** |

---

## 🔗 Related Prompts

- **Triggered by:** [P01 — Event classification](P01-event-classification.md)
- **Next in chain:** [P10 — Event closure](P10-event-closure.md)
- **Parent section:** [03-compliance-and-reporting](../workflows/03-compliance-and-reporting/README.md)
