# Week 3 Asynchronous Activity — Feedback

**Val Anthonne C. Lopez** · Case P4 — Sales and Customer Performance
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027

---

## Your mark: 59 / 100

> Your counting is now exact — every number right. Then half the activity was not handed in.

| Criterion | Score | Weight |
|---|---|---|
| Technical correctness | 3 / 4 | 35% |
| Business justification | 2.5 / 4 | 25% |
| Documentation and readability | 1.5 / 4 | 20% |
| Response to prior feedback | 2 / 4 | 15% |
| Timeliness and integrity | 2 / 4 | 5% |

**Read the next section before you look at that number again.** It went sideways from B1, and the reason is not your thinking.

---

## What you did well

**Every single number you wrote is correct.** MovementType 5, Tier 5, PaymentMethod 3, Category 5, 4,775 blank customer IDs at 45.1%, 46 duplicate rows, 10,566 remaining, 23 surplus, 12 blank dates, 23 amount mismatches. I checked every one against the source file. Not one is wrong.

In your B1 feedback I told you: *count everything, and never write "some" where a number belongs.* There is not one vague quantity anywhere in this submission. You did exactly what I asked, and it worked.

**Your verdicts explain rather than list.** On MovementType you wrote *"There should be only 4 rows but because of inconsistency the deliver/delivery became a 2 different type."* On Tier: *"There are 2 inconsistent types… The count should be only 3 tiers."* You didn't just name the offenders — you said what the number *should* be and why it isn't. That is how a finding gets written up, and it is a step beyond what the exercise asked for.

**Your predictions are honest.** You guessed 20 for Product Category and the answer was 5. You guessed 10% for blank customer IDs and it was 45%. You left both wrong guesses on the page. Five seconds of editing would have hidden them and destroyed the point of the exercise. You didn't, and I noticed.

**Part B3 is the best answer in the class.** I mean that literally.

> *"The amount column is the problem, I won't change anything. I would simply tell the branch manager that I found 23 rows that did not equal to the data quantity × unitprice. And I would suggest double checking everything before correcting the record."*

You named the suspect column, refused to alter it, reported the exact count, and recommended verification **before** correction. Another student found the same 23 rows and then attached a theory to them that only explains eleven. You didn't reach for an explanation you couldn't support. That restraint is a professional instinct and it is rarer than the technical skill.

It is also the second time you have found those 23 rows unaided. In B1 you found them when almost nobody did. That is now a pattern, and it is your strongest quality as an analyst.

**You reported honestly when the exercise didn't behave.** You wrote *"IT SHOWED NO DATA"* where the sheet promised errors. That is the correct thing to record. I was wrong on that page, not you — the conversion behaves differently depending on your regional settings.

---

## Part by part

### Part A1 and A3

Correct throughout. On A3 you chose the right number to report — the 23 surplus rows — and gave a sound reason.

You did leave half the question unanswered, though. I asked what the *first* number answers and what the *second* answers, one sentence each. You only told me which one you would report. The distinction is worth having straight: **46 tells you how many rows are involved in duplication. 23 tells you how many to delete.** Those go in different sentences of a report, and confusing them is how a fix gets over- or under-scoped.

### Part A2 — the one to think hardest about

You measured it exactly: 4,775 rows, 45.1%. Then you classified it as a data quality defect and proposed supervising data entry so the field gets filled in.

**It is not a defect.** Those are walk-in customers.

Follow your remedy through to what it would mean on the floor. To fill that field, a barista would have to ask every single person buying a coffee for identifying details before serving them — for nearly half of all transactions. Kape Tayo would lose customers over it, and the data would still be poor because people would refuse or invent answers.

Ask the diagnostic question before reaching for a fix: **is this field missing, or was it never applicable?** A loyalty ID is only meaningful when the buyer is in the loyalty program. Absence *is* the information — it tells you 45% of your sales are anonymous walk-ins, which is a genuinely useful fact about the business.

The right response is not to fill it. It is to write one sentence in your documentation: *customer-level analysis covers 55% of transactions; branch, product and time analysis cover 100%.* That sentence protects every report you build afterward.

You did get the important part right — **you refused to delete the rows.** Deleting them would have erased 45% of the company's revenue. Your instinct was protective even though your classification was off.

### Part B1

12 blank dates. Correct.

### Part B2 — incomplete

Both boxes are blank, and you didn't answer which of the two sequences works.

You hit a real problem: the errors the sheet promised never appeared. But then you stopped. **The activity told you: fifteen minutes, then message me.** You had my number, it was a weekend, and I was checking messages. Two minutes of my time would have unblocked you and this section would have been complete.

For the record, so you have it: the correct order is **Sequence 2 — Replace Values first, then change type.** The values are text like `4,195`; the comma has to go before the conversion can succeed. On your machine the conversion handled the comma automatically, which is why nothing broke — but write the Replace step anyway, because on a machine with different regional settings it *will* break, and your query has to survive being opened by someone else.

### Part C — not attempted

This is where most of the mark went. Your exported model contains no steps at all:

```m
let
  Source = Excel.Workbook(File.Contents("C:\Users\anthonne lopez\Downloads\KapeTayo_IntegratedCase.xlsx"), null, true),
  #"Navigation 1" = Source{[Item = "tblSales", Kind = "Table"]}[Data]
in
  #"Navigation 1"
```

Source, navigate, done. No date type change, no duplicates removed, no Check column — even though your answers prove you performed all three. You did the work in the editor, read the numbers off the screen, and then discarded it.

Part C is 20% of the rubric on its own. It is the part I told you was graded most heavily.

### Part D — one table instead of seven

Only `tblSales` was exported. The backup should carry the whole model, and in any case a backup of a model with no work in it restores you to nothing.

Two other things in that export worth knowing about:

**Your source is a file on your own laptop.** `File.Contents("C:\Users\anthonne lopez\Downloads\...")`. That path exists only on your machine, so this model can never refresh in the Power BI Service — it would have to be able to reach your Downloads folder. Point it at the copy in your OneDrive instead. This becomes a hard blocker in Week 12 when we set up scheduled refresh, so fix it now while it is a two-minute job.

**Your Windows username is in a file you committed to a shared repository.** Small thing, and no harm done here. But get in the habit of looking at what a file reveals before you push it — in this course we are about to spend a week on data privacy, and the principle is the same.

### Part E — not submitted

The reflection is missing. It carries the two questions that measure whether the week actually landed: which of your decisions was a judgement call rather than a correction, and what you found this week that you missed in B1.

---

## Where to push next

- **Save your work before you close the editor.** Every number in this submission was correct and none of it survived. The steps *are* the deliverable — not the numbers you read off them.

- **Point your source at OneDrive, not `C:\Users\...`.** Two minutes now, a blocked week later.

- **Finish the sheet before you submit it.** In your B1 feedback I wrote: *reread the brief before submitting and tick off each requirement.* B2 has blank boxes, C is missing, E is missing. This is the same thing costing you marks two weeks running, and it has nothing to do with ability.

- **Use the fifteen-minute rule.** You got stuck in B2 and stayed stuck. Message me. It costs me two minutes and it costs you a section.

- **Ask "missing or not applicable?" before proposing a fix.** That single question would have turned A2 around.

---

## Closing

Two things happened here, and they pull in opposite directions.

The first is that **you did exactly what I asked you to do.** B1 said count everything and stop writing "some." Every number in this activity is exact and correct, including the ones that took real work to get. And your Part B3 answer is better than anyone else's in this class — you found something ambiguous and had the discipline not to explain it away. Both of those are the analyst's job, and both of them are getting stronger.

The second is that **the same thing that cost you marks in B1 cost you marks again.** Not the thinking. The finishing. Three sections were left incomplete or unsubmitted, and I had already told you, in writing, to check the brief before handing in.

So the mark did not move, but the reason it did not move is completely different from last time. In B1 the concern was whether your findings were specific enough. That concern is gone. What is left is a habit — starting well and not carrying through to the end — and habits are far easier to fix than judgement.

Here is what I want. **Finish Part C and Part E and send them to me by Saturday.** I will not re-mark the activity, but I want to read them, and I want you to have the experience of handing in something complete. You are one habit away from a mark that matches how you actually think.

— Sir JB
