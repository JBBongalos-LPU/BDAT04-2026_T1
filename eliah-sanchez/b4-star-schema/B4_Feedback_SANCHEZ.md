# B4 — Star Schema Build

**Eliah Therrien E. Sanchez** · Case P5 — Profitability
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027
Session 7, asynchronous · marked 10 October 2026

---

## Mark: 43.75 / 100 — provisional

*The right instincts, again. The activity sheet never arrived, and that is where most of the marks lived.*

**Read the last section before you read anything else. This mark can move.**

---

## Rubric D

| Criterion | Weight | Level | Why |
|---|:--:|:--:|---|
| Technical correctness | 35 | **2** | `dimDate` built correctly at 730 rows — but connected to nothing, missing `Quarter`, and a stray `Query1` left in the model. |
| Business justification | 25 | **1** | No sheet, so no grain statements, no analysis and no reflections to assess. |
| Documentation and readability | 20 | **2** | Screenshots clear and the backups are exemplary. Filed inside an undeclared `S7/` subfolder, stray query left behind. |
| Response to prior feedback | 15 | **2** | Both TMDLs submitted, including the pre-activity backup nobody else took. The written work did not come. |
| Timeliness and integrity | 5 | **2** | No AI Use Log entry for B4. |

Σ(level × weight) ÷ 4 = **43.75**

---

## What you did, and I want you to hear this first

Teyen — **you are the only student in this class who took the pre-activity backup.**

Page 1 of the sheet asked everyone to export the model to TMDL *before touching anything*, and save it as `model_2026-10-08_before.tmdl`. Four people read that instruction. One person did it. Your folder has both the before and the after, exactly as asked.

In your last letter I wrote that you read the instruction and did the thing — the only one who drew the schema on paper — and I asked you to do that with the file names too. **You did it again.** That is twice now that the most careful piece of work in the class has been yours.

Your `dimDate` is built correctly: the right M expression, the right range, 730 rows, 1 January 2025 through 31 December 2026. The build itself is sound.

---

## What is missing, plainly

**There is no activity sheet.** Items 1 through 7 — every grain statement, every analysis, every reflection — are the bulk of this milestone, and there is nothing to mark. That is where forty points went.

**Your `dimDate` is connected to nothing.** It sits in the corner of your model view with no relationships at all, and so does `tblCalendar`. Item 6 asked you to wire the star — delete the old calendar relationships, connect both fact tables to `dimDate`, set cardinality and filter direction deliberately. None of that happened. You built the table and stopped.

**No `Quarter` column** on `dimDate`, and a stray **`Query1`** table left in the model.

**No AI Use Log entry** for B4.

---

## Why I am calling this provisional

Here is what I actually think happened, and I would rather ask you than assume.

You organised your work into an `S7/` subfolder with a `backups/` folder inside it. You took the pre-activity backup. You built the date table with the correct expression. **That is not the behaviour of somebody who did not do the work. That is the behaviour of somebody who ran out of Friday.**

So I am asking you directly, and there is no wrong answer:

- **Does the sheet exist?** If you filled it in and did not upload it, say so and upload it. I will mark it.
- **Did you run out of time before Item 6?** Say that instead. That is an honest answer and I will treat it as one.

What I do not want is for you to say nothing and let 43.75 stand when the work might be sitting on your laptop. Message me in the group chat or directly, before Wednesday.

---

## When you come back to it

Whatever the answer, do this one thing: **connect `dimDate` to `tblSales` and `tblInventory`, many-to-one, single direction.** Then go and look at your orphan counts. The 82 inventory orphans you found in Week 4 will be gone — not reduced, gone — because the two dates your old calendar was missing, 15 January and 1 September 2025, are now in the table. Watching that number drop to zero is the whole point of this milestone and I would hate for you to miss it.

Then delete `Query1` and add the `Quarter` column while you are in there.

B5 is DAX measures and filter context, due noon Friday 16 October, and it needs a wired model to work at all. Get the star connected first — everything in B5 depends on it.

---

Your W4 append once ran the July file against itself, and the method was right while the first step was wrong. This is the same shape: the care is right, the finish did not land. You do not have a thinking problem. You have a last-twenty-minutes problem, and that one is fixable.

**Tell me whether the sheet exists. That is all I need from you today.**

*Jerald B. Bongalos · Course Facilitator, BDAT04 · College of Business and Accountancy, LPU – Laguna*
