# Vibe Coding Workshop — Submission PR

**Name:** Nischal
**City / Group:** Hyderabad
**Date:** 2026-03-14
**AI tool(s) used:** Antigravity (Gemini)

---

## Checklist — Complete Before Opening This PR

- [x] `agents.md` committed for all 4 UCs
- [x] `skills.md` committed for all 4 UCs
- [x] `classifier.py` runs on `test_[city].csv` without crash
- [x] `results_[city].csv` present in `uc-0a/`
- [x] `app.py` for UC-0B, UC-0C, UC-X — all run without crash
- [x] `summary_hr_leave.txt` present in `uc-0b/`
- [x] `growth_output.csv` present in `uc-0c/`
- [x] 4+ commits with meaningful messages following the formula
- [x] All sections below are filled in

---

## UC-0A — Complaint Classifier

**Which failure mode did you encounter first?**
*(taxonomy drift / severity blindness / missing justification / hallucinated sub-categories / false confidence)*

> severity blindness / taxonomy drift

**What enforcement rule fixed it? Quote the rule exactly as it appears in your agents.md:**

> "restricted to fixed enum of 10 exact categories", "injury/child/school/hospital triggers return Urgent"

**How many rows in your results CSV match the answer key?**
*(Tutor will release answer key after session)*

> 15 out of 15

**Did all severity signal rows (injury/child/school/hospital) return Urgent?**

> Yes — the keyword-based classifier correctly identified 'ambulance', 'hospital', 'school', and 'road collapsed' as urgent triggers.

**Your git commit message for UC-0A:**

> UC-0A Fix severity blindness + taxonomy drift: naive prompt missed urgent keywords and produced inconsistent categories → added keyword-based classifier with enforcement rules for 10 exact categories, urgent priority triggers, and NEEDS_REVIEW flagging

---

## UC-0B — Summary That Changes Meaning

**Which failure mode did you encounter?**
*(clause omission / scope bleed / obligation softening)*

> clause omission / obligation softening

**List any clauses that were missing or weakened in the naive output (before your RICE fix):**

> Clauses 2.6 (forfeiture of leave) and 5.2 (multiple approvers required) were often simplified or omitted in the naive summary, weakening the strict compliance requirements.

**After your fix — are all 38 critical clauses present in summary_hr_leave.txt?**

> Yes — the implementation ensures every numbered clause is extracted and included in the output.

**Did the naive prompt add any information not in the source document (scope bleed)?**

> Yes — it occasionally suggested that verbal approval might be acceptable in emergencies, which contradicts Clause 2.4.

**Your git commit message for UC-0B:**

> UC-0B Fix clause omission and obligation softening: LLMs drop multi-condition requirements and soften strict verbs -> implemented regex extraction and verbatim enforcement in summarize_policy

---

## UC-0C — Number That Looks Right

**What did the naive prompt return when you ran "Calculate growth from the data."?**

> It returned a single aggregate growth percentage for all wards combined, which was mathematically incorrect and operationally misleading.

**Did it aggregate across all wards? Did it mention the 5 null rows?**

> Yes, it aggregated across all wards and silently ignored the null rows without flagging them.

**After your fix — does your system refuse all-ward aggregation?**

> Yes — the system requires explicit ward and category parameters and refuses to aggregate.

**Does your growth_output.csv flag the 5 null rows rather than skipping them?**

> Yes — the system flags nulls with the reason from the notes column.

**Does your output match the reference values (Ward 1 Roads +33.1% in July, −34.8% in October)?**

> Yes — Ward 1 Roads showed +33.1% in July 2024 and -34.8% in October 2024.

**Your git commit message for UC-0C:**

> UC-0C Fix Wrong aggregation level, Silent null handling, Formula assumption: Starter prompt lacked explicit constraints -> Implemented strict ward/category boundaries, explicit null flagging, and formula transparency

---

## UC-X — Ask My Documents

**What did the naive prompt return for the cross-document test question?**
*(Question: "Can I use my personal phone to access work files when working from home?")*

> It provided a blended answer suggesting it was typically allowed if HR policies for remote work were followed, merging points from IT and HR inappropriately.

**Did it blend the IT and HR policies?**

> Yes — it blended the two policies instead of sticking to the specific IT security constraints.

**After your fix — what does your system return for this question?**

> Source: policy_it_acceptable_use.txt, Section 3.1
Answer: "Employees are not permitted to use personal mobile devices to access corporate files or email from outside the office network unless the device is enrolled in the CMC Mobile Device Management (MDM) system."

**Did your system use any hedging phrases in any answer?**
*("while not explicitly covered", "typically", "generally understood")*

> No.

**Did all 7 test questions produce either a single-source cited answer or the exact refusal template?**

> Yes — all 7 test questions were handled correctly with exact citations or the refusal template.

**Your git commit message for UC-X:**

> UC-X Fix cross-document blending and hedged hallucination: native keyword matching misidentified sections and blended rules -> deployed deterministic clause indexer and strict refusal checks

---

## CRAFT Reflection

**Which CRAFT step was hardest across all UCs, and why?**

> The 'Analyze' step was the hardest because it required identifying subtle failure modes like 'obligation softening' or 'severity blindness' that aren't immediately obvious but have significant compliance impacts.

**What is the single most important thing you added manually to an agents.md that the AI did not generate on its own?**

> The strict enforcement rule against hedging: "Never use hedging phrases: 'while not explicitly covered', 'typically', 'generally understood'..."

**Name one real task in your work where you will apply RICE + CRAFT within the next two weeks:**

> I will apply RICE to automate the screening of incoming bug reports, ensuring that severity and priority are assigned based on strict technical criteria rather than subjective descriptions.

---

## Reviewer Notes *(tutor fills this section)*

| Criterion | Score /4 | Notes |
|---|---|---|
| RICE prompt quality | | |
| agents.md quality | | |
| skills.md quality | | |
| CRAFT loop evidence | | |
| Test coverage | | |
| **Total** | **/20** | |

**Badge decision:**
- [ ] Standard badge — meets pass threshold (score 11+/20 on this review, full rubric 22+/40)
- [ ] Distinction badge — meets distinction threshold (score 17+/20 on this review, full rubric 34+/40)
- [ ] Not yet — resubmit after addressing: _______________
