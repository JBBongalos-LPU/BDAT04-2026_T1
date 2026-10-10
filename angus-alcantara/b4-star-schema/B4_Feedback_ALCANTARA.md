# B4 — Star Schema Build

**Angus Jullian G. Alcantara** · Case P6 — Workforce
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027
Session 7, asynchronous · marked 10 October 2026

---

## Mark: 82.5 / 100

*The best work you have produced in this course, and the first time your model has caught up with your writing.*

---

## Rubric D

| Criterion | Weight | Level | Why |
|---|:--:|:--:|---|
| Technical correctness | 35 | 3 | `dimDate` correct at 730 rows and accepted as a date table; every relationship deliberate; validation exact. Held at 3 by the missing attribute columns. |
| Business justification | 25 | **4** | The `City → City` reflection and the blank-customer answer are both exemplary — business reasoning, not model mechanics. |
| Documentation and readability | 20 | 3 | Sheet fully completed, screenshots legible, AI log specific. The TMDL export is incomplete and the folder still holds a B3 file. |
| Response to prior feedback | 15 | 3 | TMDL submitted, AI log now thorough. Filing drift persists. |
| Timeliness and integrity | 5 | **4** | Honest, specific, per-stage AI log. |

Σ(level × weight) ÷ 4 = **82.5**

---

## What you did well

AJ — in your last letter I told you your writing was already at the level this course is aiming for, and asked you to make the model agree with it. **You did.** I want to say that plainly before anything else, because it is the thing that happened here.

**Your Item 7 is the best piece of analysis anyone has handed me this term.** You did not just report orphan counts — you took every single one, set it beside your own Week 4 figure, and explained the difference in business terms. The 66 branch orphans and the 1 employee orphan both went to zero *because B07 now exists in `tblBranches`*. The 82 inventory orphans resolved *because `dimDate` closed the gaps the old calendar had*. The 5,039 blanks and the 8 true orphans stayed, and you knew why they were different animals. That is not a student checking boxes. That is somebody reading a model.

Your total came out at ₱2,694,600.80, exact.

**And Item 1 is the sharpest thing anyone wrote.** Power BI had auto-detected `tblCustomers[City] → tblBranches[City]`, and you saw immediately why that is wrong: a customer from one city buys at several branches, so filtering sales by branch would quietly distort customer revenue. You reasoned from the coffee shop, not from the software. That is the whole subject in one paragraph.

Your grain statements carry proof rows. Your Item 4 transcription is word for word. Your AI log is honest and specific about what you asked and how you checked it.

---

## Two things to fix, and one is quick

**Your `dimDate` appears to have only a `Date` column.** Item 5.3 asked for Year, Quarter, Month number, Month name, Day and Day of week name, and your sheet never claims you added them — your model view shows one column. Open the field list and check. If they are there, tell me and I will revise this mark upward today.

If they are not: **this one bites in Week 10.** Time intelligence needs a hierarchy to work across. A date table with only dates gives you nothing to slice by, and you will be rebuilding it under time pressure in three weeks instead of in five quiet minutes now.

**Your TMDL export contains eight tables but not `dimDate`.** You exported before you built it, or copied only some scripts. Your model view proves the table exists and is wired, so I am not questioning the work — but the export is supposed to be the evidence, and right now it evidences a model you no longer have. Re-export and commit it.

**Filing.** Your B3 activity sheet is still sitting in `b4-star-schema/`. Third time I have mentioned this. Move it to `b3-model-design/` and the problem is gone forever.

---

## Before B5

B5 is DAX measures and filter context, due noon Friday 16 October. One thing to carry in: **you cannot write a measure over a column that is stored as text.** Your `tblSales` once had `Quantity`, `UnitPrice`, `Amount` and `Check` all left as `string`, and nothing in your written work revealed it. Before you write a single measure, open the field list and look at the data types. Five minutes.

And read the AI rule on page 1 of the B5 sheet carefully. It concerns Copilot, and it applies to you more than anyone because you are the student most likely to be offered a correct answer and most able to tell whether it is one.

---

You led the written half of both exams and I kept telling you the gap was execution. This milestone is the first one where I cannot say that. Keep the model honest and the rest of this course belongs to you.

**Now go and check those columns.**

*Jerald B. Bongalos · Course Facilitator, BDAT04 · College of Business and Accountancy, LPU – Laguna*
