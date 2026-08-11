# P01 · Corporate action event classification

**Section:** 01 — Event Classification & Notification

**Workflow step:** Step 1 of 3

**Current version:** v1.4

**Status:** ✅ Tested and approved

**Last updated:** August 2026

---

## 📌 Prompt Text (v1.4 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a corporate actions analyst at an investment banking company.
Review the raw event feed entry and classify the event as either
Mandatory or Voluntary. Then identify which client-notification
fields are still missing.

You will be given a raw event feed entry. Fields may be separately
labelled (e.g. "RECORD DATE:", "PAYMENT DATE:") or may appear
combined under a single generic label (e.g. "KEY DATES:"). Use only
the information provided in the feed.

First, state the classification: Mandatory or Voluntary.

Then check the feed against this fixed list of required fields only
— do not introduce any other categories:
- Record date
- Payment date (or settlement date, for mergers)
- Exchange ratio or consideration amount
- Instruction deadline (Voluntary events only)

For each field, state exactly one of: Present, Missing, Ambiguous, or
Not Applicable.
- If a field is separately and clearly labelled in the feed, mark it
  "Present" and state its value.
- If a field is required for this event type but no relevant data is
  provided, mark it "Missing."
- If data is provided but combined under a single generic label so it
  cannot be confidently mapped to one specific field, mark it
  "Ambiguous" and state the value provided.
- The "Instruction deadline" field applies only to Voluntary events.
  If the event is classified as Mandatory, always mark this field
  "Not Applicable" — never "Missing" — regardless of whether
  deadline data appears in the feed.

Do not invent missing data, and do not add fields outside this list.
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[ISIN]` | Corporate action notice / security details | US0378331005 |
| `[EVENT_TYPE_CODE]` | Event classification field | MRGR (Merger) |
| `[RECORD_DATE]` | Corporate action event dates | 15.08.2026 |
| `[PAYMENT_DATE]` | Corporate action event dates | 22.08.2026 |
| `[TERMS]` | Event terms / offer conditions | Cash merger at USD 25.00 per share |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 1** of the corporate actions processing chain.

- **Trigger:** Custodian/data feed delivers a new corporate action record
- **Actor:** Corporate actions analyst (reviews and routes output)
- **Timing:** Same day the feed record is received
- **Next step:** Mandatory → P02. Voluntary → P03.

```
Custodian data feed (labelled or combined format)
    |
    v
P01 v1.4 runs
    |
    v
Classification determined: Mandatory or Voluntary
    |
    v
Each required field checked against feed data:
    |
    +-- Field separately labelled in feed --------------> Present (value shown)
    |
    +-- Field required but no data at all ---------------> Missing
    |
    +-- Data present but under a combined/generic
    |    label, type cannot be confidently mapped -------> Ambiguous (value shown, type noted as unclear)
    |
    +-- Instruction deadline field, but event is
         classified Mandatory --------------------------> Not Applicable (rule-based, not inferred)
    |
    v
Officer reviews classification + field checklist
    |
    +-- Mandatory --> P02 (client notification drafted using confirmed fields)
    |
    +-- Voluntary --> P03 (notification + instruction request, using confirmed
                        fields and instruction deadline if Present)
```

---

## ❗ Problem Being Solved

Officers manually cross-check feed data against a classification checklist for every one of ~150 monthly corporate action events, roughly 5 minutes each just for triage — about 12.5 hours per month across the desk.

**Pain points addressed:**
- Misclassification risk when done under time pressure
- Missing or ambiguous fields discovered late, delaying notification drafting
- Inconsistent triage quality between officers
- Silent handling of ambiguous data (a date present but unmapped to a specific field) if not explicitly checked for

---

## ⚡ Automation Potential

**Level: High**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | Very high — same structure every time |
| Data availability | All fields exist in the custodian feed |
| Human judgment needed | Low — edge cases and final sign-off only |
| Integration possibility | Could trigger automatically from the feed ingestion system |
| Estimated time saving | ~80% (5 min → ~1 min including review) |

**Human-in-the-loop role:** Officer confirms classification and reviews the field-status checklist (Present/Missing/Ambiguous/Not Applicable) before the event proceeds to drafting.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| Misclassification (Mandatory vs Voluntary) | Medium | Spot-checked against the custodian's official event type code before proceeding |
| Ambiguous data silently treated as missing | Medium (resolved in v1.2) | Explicit "Ambiguous" status added so unmapped-but-present data is surfaced, not discarded |
| Inference-based correctness not guaranteed to repeat | Medium (resolved in v1.4) | Instruction deadline handling for Mandatory events made an explicit rule rather than left to model inference |
| Model expands checklist scope beyond intended fields | Low (resolved in v1.1) | Fixed field whitelist introduced; model instructed not to add categories outside it |

**Overall risk rating: LOW–MEDIUM** — misclassification and silent data loss would change downstream notification accuracy, so this step always receives a human review before the event proceeds to drafting.

---

## 🔄 Version History

### v1.0 — Initial draft

**Date:** 10.08.2026

**Prompt:** Classify this event as Mandatory or Voluntary, then list missing fields for a client notification. Do not invent missing data.

**Output:** Classification correct (Mandatory), no invented dates — but the missing-fields checklist expanded to 7 items, including categories outside the intended scope (tax implications, contact information, holdings impact).

**Observed effect:** Output was accurate but unpredictable in scope — different runs could flag different "extra" categories depending on the model's own judgement of what a notification "needs."

**Lesson learned:** v1.0 revealed that the model's definition of "missing fields" was broader than P01's intended scope within the workflow — it reasoned about notification completeness in general, not specifically about the event-variable data P02/P03 require.

---

### v1.1 — Constrained checklist to a fixed field whitelist

**Date:** 10.08.2026

**Change:** Replaced the open-ended "provide a checklist of missing fields" instruction with a fixed list of four required fields (record date, payment/settlement date, exchange ratio or consideration amount, instruction deadline) and an explicit instruction not to introduce fields outside this list.

**Output:** Classification correct (Mandatory). All four whitelisted fields addressed individually — record date and payment date both flagged as missing, exchange ratio correctly identified as present, and the instruction deadline field correctly marked "Not applicable" rather than "missing," since the model recognised it only applies to Voluntary events.

**Observed effect:** Output scope became fully predictable — exactly 4 fields addressed, zero categories outside the whitelist. However, the model silently disregarded the single date provided in the feed ("KEY DATES: 15.08.2026") rather than flagging it as ambiguous — it did not attempt to map this date to record date or payment date, nor did it note that a date was present but its type was unclear. Both fields were marked "missing" as if no date data existed at all.

**Lesson learned:** A closed field list controls scope effectively but does not by itself teach the model to reconcile ambiguous input against that list. A stronger v1.2 would explicitly instruct the model to flag ambiguous-but-present data (e.g. "if a date is provided but its type is unclear, state this explicitly rather than marking the field as missing") rather than silently treating it as absent.

---

### v1.2 — Added explicit "Ambiguous" status for unmapped data

**Date:** 10.08.2026

**Change:** Extended field status from a binary Present/Missing to three states (Present, Missing, Ambiguous), and added an explicit instruction: if a date is provided but its specific field type cannot be determined, mark it "Ambiguous" and state the date rather than marking the field "Missing."

**Output:** Tested against a deliberately ambiguous feed (`KEY DATES: 15.08.2026`, a single unlabelled date field). Record date and payment date were both correctly returned as "Ambiguous (15.08.2026 provided, but it is unclear if this is the record date or another key date)." Exchange ratio and instruction deadline remained correctly classified, unaffected by the change.

**Observed effect:** The model no longer discards ambiguous-but-present data. Officers reviewing the output can now see that a date exists in the feed and needs clarification, rather than being told — incorrectly — that no date data was provided at all. However, this test also revealed a limitation in the test feed design itself: real custodian feeds always provide record date and payment date as separately labelled fields, so a single combined "KEY DATES" field does not reflect realistic input. This meant v1.2's "Ambiguous" behaviour, while correct for the input given, had not yet been validated against realistically structured data.

**Lesson learned:** Explicitly naming a third output state (Ambiguous) alongside Present/Missing closed a real gap — binary classification schemes can silently misrepresent genuinely uncertain data as confidently absent. At the same time, this iteration surfaced a separate issue: the prompt did not yet distinguish between "data is genuinely ambiguous" and "data is separately labelled and should be read directly." This motivated v1.3, which adds explicit handling for both labelled and combined field formats.

---

### v1.3 — Added support for both labelled and combined feed formats

**Date:** 10.08.2026

**Change:** Added explicit handling for two different feed formats: separately labelled fields (e.g. "RECORD DATE:", "PAYMENT DATE:") should be read directly and marked "Present," while data combined under a single generic label (e.g. "KEY DATES:") should be marked "Ambiguous." Previously, the prompt only handled the ambiguous case.

**Output:** Tested against a realistically structured feed with separately labelled RECORD DATE and PAYMENT DATE fields. Record date, payment date, and exchange ratio were all correctly marked "Present" with their values, confirming the prompt now handles well-formed feeds correctly, not just ambiguous ones. However, the Instruction deadline field — which should logically be "Not Applicable" for a Mandatory event — was returned as "Missing" instead, despite the model having correctly inferred "Not Applicable" for the same logical situation in earlier ad hoc tests under v1.1 and v1.2.

**Observed effect:** The core Present/Ambiguous logic worked reliably once realistic data was used. However, this test surfaced a separate, previously undetected inconsistency: the model's handling of the Instruction deadline field for Mandatory events was not governed by any explicit rule in the prompt — it had only ever appeared correct "by inference," and that inference did not hold consistently across test runs.

**Lesson learned:** Correct behaviour observed in earlier tests is not proof that a prompt enforces that behaviour — it may simply reflect the model's inference on that particular run. Any field whose correct value depends on another field (here, Instruction deadline depending on the Mandatory/Voluntary classification) needs an explicit conditional rule in the prompt, not an assumption that the model will infer it consistently every time.

---

### v1.4 — Explicit rule for "Not Applicable" status ✅ Current

**Date:** 10.08.2026

**Change:** Added a fourth status option (Not Applicable) alongside Present/Missing/Ambiguous, with an explicit conditional rule: if the event is classified as Mandatory, the Instruction deadline field must always be marked "Not Applicable," never "Missing," regardless of what appears in the feed.

**Output:** Tested against the same well-formed feed as v1.3 (separately labelled record date, payment date, exchange terms). Record date, payment date, and exchange ratio were all correctly marked "Present" with their values. Instruction deadline was correctly and consistently marked "Not Applicable."

**Observed effect:** v1.3 had shown that, without an explicit rule, the model's handling of the Instruction deadline field for Mandatory events was inconsistent — it had correctly inferred "Not Applicable" in earlier ad hoc tests but returned "Missing" for the same logical situation in the v1.3 test run. Adding an explicit conditional rule removed this inconsistency: the field is now determined directly by the event classification, not left to the model's inference.

**Lesson learned:** Behaviour the model produces correctly "by inference" in some test runs is not reliable evidence that the prompt itself enforces that behaviour. Where a field's applicability depends on another field's value (here, event classification), that dependency should be stated as an explicit rule rather than left for the model to infer each time — inference-based correctness can silently regress between runs.

---

## 📊 A/B Test Results

**Test date:** 10 August 2026 | **Evaluators:** Author self-test

| Criteria | v1.0 score | v1.4 score |
|----------|------------|------------|
| Rule adherence | 2.0/5 | 4.8/5 |
| Completeness | 2.0/5 | 4.7/5 |
| Handling ambiguous data | 1.0/5 | 4.6/5 |
| Consistency across feed formats | 2.0/5 | 4.2/5 |
| Human-review readiness | 3.0/5 | 4.5/5 |
| **Overall** | **2.0/5** | **4.6/5** |

---

## 🔗 Related Prompts

- **Next in chain (Mandatory):** [P02 — Mandatory event notification](P02-mandatory-notification.md)
- **Next in chain (Voluntary):** P03 — Voluntary event notification
- **Parent section:** [01-event-classification-and-notification/README.md](../workflows/01-event-classification-and-notification/README.md)
