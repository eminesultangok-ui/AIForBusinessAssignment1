# P06 · Compliance check

**Section:** 03 — Compliance and Reporting
**Workflow step:** Step 1 of 4
**Current version:** v1.0
**Status:** ✅ Tested and approved
**Last updated:** August 2026

---

## 📌 Prompt Text (v1.0 — current)

> Copy this exactly into your AI tool. Replace all `[PLACEHOLDERS]` before running.

```
You are a compliance-aware assistant at an investment banking
company, not a legal advisor. You are reviewing a draft client email
before it is sent, to check for compliance issues — you do not write
or send emails yourself.

Using this draft client email: [email draft]

Review the email and identify, as a bullet-point list, any statements
that could be read as investment advice or a recommendation to the
client. For each flagged statement, quote the specific line and
briefly explain why it is a concern.

If no concerning statements are found, state clearly: "No compliance
concerns identified — recommend standard human review before
sending."

This review is not a final sign-off. Do not state that the email is
approved, safe, or ready to send — a qualified compliance reviewer
must always make that decision.

Do not add an analyst name — sign the report only as "Compliance
Aware Team."
```

**Placeholders to fill:**

| Placeholder | Source | Example |
|-------------|--------|---------|
| `[Email Draft]` | Email Draft | Subject: Rights Issue – AAPL-APPLE. Dear Client, We are writing to inform you about a voluntary rights issue for your holding in AAPL-APPLE. You currently hold 100 shares and are eligible to subscribe for 1 new share for every 3 shares held, at a price of USD 15.00 per new share. This is a good opportunity and we recommend you participate, as the subscription price is attractive compared to current market value. Please submit your instruction by 20 August 2026. Corporate Actions Team |

---

## 🏢 Intended Workflow or Task

This prompt is **Step 1** of the Compliance and Reporting stage.

- **Trigger:** Immediately after P02 or P03 drafts the notification, before sending
- **Actor:** Corporate actions analyst / compliance reviewer
- **Timing:** Before every client send, no exceptions
- **Next step:** Flags addressed → notification sent to client

```
P02/P03 draft --> P06 runs --> Flags found? --> Yes: revise and re-check
                                              --> No: send to client
```

---

## ❗ Problem Being Solved

Analysts occasionally include advice-adjacent phrasing without realising the compliance implication, and manual review before every send is inconsistent under time pressure.

**Pain points addressed:**
- Advice-adjacent language slipping into client-facing drafts unnoticed
- Inconsistent manual review quality across analysts
- No structured, repeatable check before every send

---

## ⚡ Automation Potential

**Level: High**

| Dimension | Assessment |
|-----------|------------|
| Repetitiveness | High — runs on every outbound notification |
| Data availability | Draft text always available from P02/P03 |
| Human judgment needed | Medium — flags require human interpretation |
| Integration possibility | Could run automatically as a pre-send gate |
| Estimated time saving | Catches recurring issues before human review starts |

**Human-in-the-loop role:** This is NOT a compliance sign-off. A qualified human reviewer remains mandatory for every email regardless of this check's output.

---

## ⚠️ Risks and Limitations

| Risk | Level | Mitigation |
|------|-------|------------|
| False negatives (misses a real issue) | Medium | Never treated as final sign-off; human reviewer always checks independently |
| False positives on neutral content | Low | Tested against a fully neutral email (P05 output) — no false flags observed |

**Overall risk rating: MEDIUM** — this is a safety-net step, not a replacement for human compliance review.

---

## 📊 A/B Test Results

**Test date:** 11 August 2026 | **Evaluators:** Author self-test

| Criteria | Clean email test (P05 output) | Flagged email test (deliberate advice inserted) |
|----------|-------------------------------|--------------------------------------------------|
| Correct detection | 5.0/5 (no false positive) | 5.0/5 (issue correctly identified) |
| Quote accuracy | N/A | 5.0/5 (exact line quoted) |
| Justification quality | N/A | 4.9/5 (specific regulatory reasoning) |
| No false sign-off language | 5.0/5 | 5.0/5 |
| **Overall** | **5.0/5** | **4.97/5** |

---

## 🔄 Version History

### v1.0 — Initial draft ✅ Current

**Date:** 11 August 2026
**Prompt:** `Review this draft client email and identify, as a bullet-point list, any statements that could be read as investment advice. Quote the line and explain why. This is not a sign-off.`
**Output:** Correctly identified the one advice-adjacent sentence, quoted it exactly, and explained the regulatory concern.
**Observed effect:** Reliable detection with no false positives — flagged the real issue, left neutral content unflagged.
**Lesson learned:** Explicit review criteria (quote + justify) produce a compliance check that adds real value rather than a generic pass/fail.

---

## 🔗 Related Prompts

- **Feeds from:** [P02 — Mandatory notification](P02-mandatory-notification.md), [P03 — Voluntary notification](P03-voluntary-notification.md)
- **Parent section:** [03-compliance-and-reporting](../workflows/03-compliance-and-reporting/README.md)
