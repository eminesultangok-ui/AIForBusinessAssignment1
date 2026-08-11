# P02 · Mandatory event notification

**Section:** 01 — Event Classification & Notification

**Workflow step:** Step 2 of 3

**Current version:** v1.1

**Status:** ✅ Tested and approved

**Last updated:** August 2026

---

## 📌 Prompt Text (v1.1 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions analyst at an investment banking company.

This event has already been classified as Mandatory by the upstream classification step.

Using this dividend event data — Security Name, ISIN, ex-date, record date, payment date, gross rate, withholding tax rate — write a
120-word client notification in plain language, sent on behalf of the bank named below.

Since this is a Mandatory event, explicitly state that no action is required from the client — the dividend will be applied automatically
to all eligible holdings.

Before drafting, check that all required fields listed above have real values (not placeholders or blanks). If any required field is
missing or clearly a placeholder, do not draft the notification — instead output only: "Missing required data: [field name]."

Do not add an analyst name — sign the notification only as "Corporate Actions Team." Do not give tax advice — direct clients to
their own tax advisor.
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[Sender Name]` | Sender Name | BLUE INVESTMENT BANKING COMPANY |
| `[Security Name]` | Security Name | AAPL-APPLE |
| `[ISIN]` | Corporate action notice / security details | US0378331005 |
| `[EX DATE]` | Corporate action event dates | 12.08.2026 |
| `[RECORD_DATE]` | Corporate action event dates | 15.08.2026 |
| `[PAYMENT_DATE]` | Corporate action event dates | 22.08.2026 |
| `[GROSS RATE]` | Event rate — before tax | $0.05/share |
| `[WITHHOLDING TAX RATE]` | Event rate — after tax | 30% |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 2** of the corporate actions processing chain (Mandatory path).

- **Trigger:** P01 classifies the event as Mandatory
- **Actor:** Corporate actions analyst (reviews and sends output)
- **Timing:** Same day as classification
- **Next step:** P06 (compliance check)

```
P01 (Mandatory) --> P02 runs --> Analyst reviews --> P06 (compliance check)
```

---

## ❗ Problem Being Solved

Near-identical drafting is repeated for every mandatory event — dividends, splits, and similar auto-applied events make up the bulk of the ~150 monthly events. Analysts also need to remember, every time, to confirm sender identity and clarify that no client action is required.

**Pain points addressed:**
- Repetitive drafting work, ~15 minutes per event
- Sender identity sometimes mixed into event data rather than treated as a fixed field
- Clients left uncertain whether they need to act on a Mandatory event

---

## ⚡ Automation Potential

**Level: High**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | Very high |
| Data availability | All fields exist in the custodian feed |
| Human judgment needed | Low — accuracy check only |
| Integration possibility | Could trigger automatically once P01 classifies |
| Estimated time saving | ~75% |

**Human-in-the-loop role:** Analyst dual-checks dates/rates against the custodian feed before send — the single highest-consequence accuracy check in the chain.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| Wrong source date propagates into client comms | Medium | Mandatory dual-check against custodian feed before send |
| Sender identity not structurally separated from event data | Low (resolved in v1.1) | Dedicated Sender field introduced; bank name no longer mixed into event data |
| Client uncertain whether action is required | Medium (resolved in v1.1) | Explicit "no action required" statement now mandated for Mandatory events |
| Missing-data fallback behaviour unverified | Low | Instruction included in prompt but not yet tested against a deliberately incomplete feed |

**Overall risk rating: LOW–MEDIUM**

---

## 🔄 Version History

### v1.0 — Initial draft

**Date:** 11 August 2026
**Prompt:** `Write a client notification email about corporate action event.`
**Output:** Accurate, well-formatted notification; correctly excluded analyst name and tax advice. But bank name was mixed into event-data fields, and no confirmation that no client action was required.
**Observed effect:** Output was constraint-compliant but incomplete — sender identity not separated, and Mandatory-event clients had no explicit "no action needed" confirmation.
**Lesson learned:** A constraint-compliant output can still miss things the constraints didn't cover — sender needed its own field, and "no action required" needed to be explicit.

---

### v1.1 — Added "no action required" statement and separated sender field ✅ Current

**Date:** 11 August 2026
**Change:** Separated bank name into a dedicated "Sender" field; added instruction to explicitly state no client action is required for Mandatory events; added a missing-data check before drafting.
**Output:** "No action is required" now appears clearly in the notification. Sender name appears naturally in the closing line rather than as a distinct header.
**Observed effect:** Client-facing clarity improved — the exact gap from v1.0 is now closed.
**Lesson learned:** Instructing the model to separate a field changes tone and placement, but doesn't guarantee a fixed structural position unless a strict format is specified.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score | v1.1 score |
|----------|------------|------------|
| Accuracy of event data | 4.5/5 | 4.7/5 |
| Constraint compliance (no analyst name, no tax advice) | 5.0/5 | 5.0/5 |
| Sender identity clarity | 3.0/5 | 4.2/5 |
| Client action clarity | 2.0/5 | 4.8/5 |
| **Overall** | **3.6/5** | **4.7/5** |

---

## 🔗 Related Prompts

- **Previous in chain:** [P01 — Event classification](P01-event-classification.md)
- **Next in chain:** [P06 — Compliance check](P06-compliance-check.md)
- **Parent section:** [01-event-classification-and-notification](../workflows/01-event-classification-and-notification/README.md)
