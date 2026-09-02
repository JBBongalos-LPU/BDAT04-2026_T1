# Week 3 Asynchronous Activity — Marking Summary

**Instructor record — not for distribution**
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027
Activity due Wednesday, 2 September 2026 · submitted to `b2-cleaned-dataset`

---

## Scores

| Student | Case | W3 | B1 | Δ | Submission status |
|---|---|---:|---:|---:|---|
| Angus Jullian G. Alcantara | P6 Workforce | **83** | 83 | — | Complete: sheet, TMDL (7 tables), reflection, AI log |
| Lawrence Lagdamen | P7 Operations | **79** | 81 | −2 | Complete: sheet, TMDL (7 tables), reflection, AI log |
| Val Anthonne C. Lopez | P4 Sales & Customer | **59** | 61 | −2 | Partial: sheet only. No reflection, no AI log, TMDL 1 table |
| Eliah Sanchez | P5 — | **—** | 67* | — | **Not submitted** |

\* Sanchez's B1 mark still requires correction from **67 → 71** — the profiling-panes instruction in the B1 brief was wrong, and she was penalised for following it. That correction is outstanding and unrelated to this activity.

**Class mean (three submissions): 73.7.** No mark moved more than 2 points from B1, but every profile changed.

### Rubric D breakdown

| Criterion | Weight | Alcantara | Lagdamen | Lopez |
|---|---|---|---|---|
| Technical correctness | 35% | 3 | 2.5 | 3 |
| Business justification | 25% | 3 | **4** | 2.5 |
| Documentation and readability | 20% | **4** | 2.5 | 1.5 |
| Response to prior feedback | 15% | 3.5 | **4** | 2 |
| Timeliness and integrity | 5% | **4** | **4** | 2 |

---

## Per-student note

### Alcantara — 83

**Remember: the discount claim.** He found the 23 Amount mismatches, refused to overwrite them, then explained them as loyalty discounts. Eleven are lower; **twelve are higher**. A discount cannot make someone pay more. He stopped one step before looking at the rows behind his own number.

His documentation is the best in the class — he wrote M comments instead of step descriptions, which is more durable than what I asked for. His fact table is entirely untyped (`Quantity`, `UnitPrice`, `Amount`, `Check` all text), so his model cannot sum revenue and he does not know it.

His predictions are honest: guessed 11 for Category, answer was 5, left it there.

**Owes me:** the negative rows explained on Saturday, the fourth reflection question, and — still open from B1 — the six uppercase emails.

### Lagdamen — 79

**Remember: he invented a method when mine failed.** B2 produced no errors on his machine. Rather than stopping, he grouped `QuantityMoved` by value, counted, and filtered to Count = 1 — reasoning that corrupted bulk figures are large and unique. His method returns fifteen candidates; he reported fourteen, having correctly discarded a legitimate −15. That is the strongest single piece of work this week.

**And he left every investigation inside the model.** `tblSales` is now **23 rows** (filtered to `[Check] <> 0`). `tblInventory` is **15 rows and 2 columns** (the Group By was never removed). His reflection describes removing the duplicates; his model contains no `Table.Distinct` step.

The B1 reporting gap closed completely — every number counted, every field filled, AI log corrected in both ways I asked. Business justification and Response to prior feedback are the two highest scores on the activity.

**Owes me:** corrected TMDL by Saturday, and the fourth reflection question. **Asked to present his B2 method on Saturday — with an explicit opt-out.** Confirm before announcing it to the class.

### Lopez — 59

**Remember: the same failure as B1, one week later.** Every number he wrote is correct — a direct, successful response to "count everything, stop writing *some*." Then Part C was not attempted at all, Part E was not submitted, and B2 was left blank.

His exported model is `Source → Navigation`. Nothing else. He performed the date change, the duplicate removal and the Check column — his answers prove it — and saved none of it.

**His Part B3 is the best answer in the class.** He named Amount as suspect, refused to change it, and said verify before correcting. He did not attach a theory he could not support, which is exactly where Alcantara went wrong.

Two technical flags: his source is `File.Contents("C:\Users\anthonne lopez\Downloads\...")`, so the model can never refresh in the Service — a hard blocker in Week 12. And his Windows username is now in a file committed to a shared repo.

He also misclassified the blank customer IDs as a defect and proposed supervising data entry.

**Owes me:** Parts C and E by Saturday (unmarked), and an AI Use Log — missing for the second milestone running.

### Sanchez — no submission

No contact and no submission. Given she scored 67 on B1 and was **unfairly marked down** on the profiling-panes instruction, the risk is that she has read a low mark, hit the same B2 confusion the others hit, and disengaged.

**Action: reach her before Saturday, and lead with the B1 correction, not the missing work.** Telling her the 67 was wrong and should be 71 changes the tone of the conversation entirely. Find out whether this is workload, a technical block, or something outside the course.

---

## What the class picture says

**1. The counting technique landed completely.** Every student who submitted got every count right — 5, 5, 3, 5, 4,775, 46/23, 10,566, 12, 23. Not one arithmetic error across three submissions. That was the pedagogical goal of Week 3 and it is achieved. Say so on Saturday.

**2. Nobody kept a clean model.** Three different failure modes, one root cause:

| Student | What they left behind |
|---|---|
| Alcantara | Fact table untyped — arithmetic worked, model cannot aggregate |
| Lagdamen | Investigations left in — two tables destroyed |
| Lopez | Nothing saved at all — model is the raw import |

None of them yet distinguishes **investigating** from **deciding**. A count is read and undone; a decision is kept and named. This needs an explicit ten minutes at the start of Week 4, and it is more important than anything else on the Week 4 agenda.

**3. My B2 instruction was wrong and it affected all three.** The type conversion is locale-dependent; under en-US the commas parse cleanly and no error appears. Their responses discriminate usefully:

- **Lagdamen** built an alternative method and validated its output
- **Alcantara** reasoned it through and wrote the Replace step anyway, for portability
- **Lopez** stopped, left the boxes blank, and did not message me

That is a resilience gradient, and it is worth more diagnostically than the exercise would have been if it had worked. Own the error to the class — it costs nothing and it models what I keep asking them to do.

**4. "Missing or not applicable?" split the class.** Lagdamen and Alcantara classified the blank customer IDs correctly and proposed documenting the meaning. Lopez called it a defect and proposed supervising data entry — which in practice means interrogating every walk-in customer. Five minutes on Saturday.

**5. Reflection completion is weak.** Nobody answered *"what did you find today that you missed completely in B1?"* — the question that measures whether the week landed. Lopez submitted no reflection at all. Consider making the reflection a separate graded line item from B3 onward rather than a component buried in the sheet.

**6. AI logs are improving.** Lagdamen fixed both faults from B1 (Tier column filled, one entry per distinct use). Alcantara's remains exemplary. Lopez has now missed it twice — that is a pattern, not an oversight, and should be raised directly rather than through the rubric.

---

## Actions arising

| # | Action | By |
|---|---|---|
| 1 | Contact Sanchez — lead with the B1 correction 67 → 71 | Before Saturday |
| 2 | Issue Sanchez's corrected B1 mark and rewrite the profiling paragraph in her letter | Outstanding since Week 2 |
| 3 | Confirm Lagdamen is willing to present his B2 method before announcing it | Before Saturday |
| 4 | Correct the B1 Milestone Brief — it still instructs students to use profiling panes that do not exist in the Service | Outstanding |
| 5 | Correct the activity sheet's B2 answer for the archive — mark on method, not on whether errors appeared | Low priority |
| 6 | Week 4 opening: ten minutes on investigation vs decision, using all three models as anonymised examples | Saturday |
| 7 | Five minutes on "missing or not applicable" | Saturday |
