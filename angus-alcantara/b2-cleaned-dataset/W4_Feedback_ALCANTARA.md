# B2 — Cleaned and Documented Dataset · Week 4 Feedback

**Angus Jullian G. Alcantara** · Case P6 — Workforce
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027

---

## Your mark: 81 / 100

> You fixed the model. You did not finish the sheet — and one answer on it contradicts your own notes.

| Criterion | Score | Weight |
|---|---|---|
| Technical correctness | 3 / 4 | 35% |
| Business justification | 3.5 / 4 | 25% |
| Documentation and readability | 3.5 / 4 | 20% |
| Response to prior feedback | 3 / 4 | 15% |
| Timeliness and integrity | 3.5 / 4 | 5% |

*B1 83 · W3 83 · B2 81. Steady, and the reasons keep changing.*

---

## What you did well

**Your model is clean now.** No leftover diagnostic queries, no investigation steps parked in a table. Last week I wrote that a model should end the day holding your decisions and not your questions. This one does. That was the single most important thing to fix and you fixed it.

**Every table runs on the parameter.**

```m
Source = Excel.Workbook(Web.Contents(SourcePath & "KapeTayo_IntegratedCase.xlsx"), null, true)
```

Eight queries, one path, one edit. That is how a model becomes portable, and you applied it consistently rather than to the one table you happened to be looking at.

**You went back for `YearMonth`.**

```m
// Changed back to Text to preserve the original month label and avoid unwanted date transformations.
#"Set YearMonth to Text type" = ...
```

In your Week 3 letter I asked you to check what had happened to that column, because `2025-01` is a month label and your model had turned it into a specific day. You found it, reversed it, and left a comment explaining why. **That is exactly what "response to prior feedback" means** — not just accepting the correction but recording the reasoning so nobody undoes it later.

**The query folding answer is the best thing in the submission, and nobody asked you for it.**

> *"Query folding only works when the source system has an active database engine like SQL that can execute transformation commands at the server level… we are only getting the data from excel with the web links so there is no database engine at the source."*

That is correct, and it goes further than the session did. I taught folding as a principle. You worked out that **it does not apply to this pipeline at all** — flat Excel files have nothing to fold back to. Most people carry the rule around for years without noticing when it stops being relevant. You noticed in a week.

**Your commented M is now the class standard.** Every consequential step carries a `//` line explaining the decision, including the row arithmetic on the append. A colleague could inherit this file.

---

## Part by part

### Append

601 rows, 11,167 after, columns went to 10. All correct, and your reason for renaming rather than deleting — *"it hold the same fact and deleting it would remove a legitimate data"* — is right.

### The integrity lab — and the contradiction

Five of six correct: 66, 9, 771, 82, 1.

The sixth says this:

| Relationship | Orphan rows found |
|---|---|
| tblSales → tblCustomers | **0** |

**It is not zero. It is 5,047.**

And you know that, because your own transformation notes say so:

> *"Decision: Keep the 5,039 null values in the CustomerID column."*

You computed the number, you made a decision about it, you wrote that decision down — and then you recorded `0` on the sheet. Two documents in the same submission disagree with each other, and the one I mark first is the one that is wrong.

There is a real distinction hiding in that zero, and it is worth getting right. The anti join returns **5,047** rows. Of those, **5,039 are blank** — your walk-ins, correctly kept. But **8 are not blank at all.** They carry `C0182`, `C0183` and `C0184`, arrived with the July file, and those three IDs do not exist in `tblCustomers`.

Your notes do reach for them — *"ACCEPT… new July CustomerIDs from July"* — so you saw something. But you never counted them and never named them. **Eight genuine orphans in the customer relationship, and your sheet records the relationship as clean.**

I would have taken ESCALATE over ACCEPT there, incidentally. A new branch opening is a documented business event you can point to. Three customer IDs appearing from nowhere is not — they could equally be a keying error at the till.

### The distinct values table

Blank. So is section 2b. The instruction was to write down the offending *values*, not only the counts, because a number tells you how big a problem is and the values tell you what it is. Had you filled that table in, you would almost certainly have caught the 8.

### Orphan decisions

*"The branch B07 and the missing Calendar dates"* — correct, and the answer I was looking for. Both are cases where the fact is real and the reference table is behind.

---

## Where the marks went, and it is the third time

`tblSales` in your submitted model:

| Column | Type |
|---|---|
| Quantity | **string** |
| UnitPrice | **string** |
| Amount | **string** |

I raised this in your Week 3 letter under "where to push next," as the first item. The laboratory sheet raised it again in step 0.4 — *set the data type of every column you will join on; a text key will not reliably match a numeric one.* It is still text.

Your model still cannot total its own revenue. Every measure in Week 8 depends on `Amount` being a number, and B5 is five weeks away.

There is a second, smaller version of the same thing: your July source points at `KapeTayo_Sales_Jul2026 1.xlsx`. That trailing ` 1` is a duplicate download. Rename the file and the query breaks — which is precisely the fragility the parameter was meant to remove.

---

## Where to push next

- **Type `Quantity`, `UnitPrice` and `Amount`. Today.** Three clicks. It has now been outstanding for three milestones and it becomes a hard blocker in Week 8.
- **Fix the customer row on your sheet** to read 5,047 = 5,039 blanks + 8 orphans, and record a decision for the 8.
- **Fill in the values, not just the counts.** The blank table is where your missed finding was hiding.
- **Rename the July file** to drop the ` 1`, and re-point the query.

---

## Closing

Three milestones, three marks within two points of each other, and a completely different reason each time. B1 was completeness. Week 3 was reading the evidence behind your own number. This one is the sheet not keeping up with the model.

That last one is the least serious of the three and the easiest to fix, because the thinking is all there — it is in your notes, in your comments, in the folding answer you were not asked for. What is missing is the discipline of making the record agree with the work. A submission where two documents contradict each other is not a small clerical matter: in a workplace, the reader has no way to know which one to believe, and the safe assumption is neither.

**Your model is now the most professional in the class.** Get the paperwork to the same standard and the mark will move, because nothing else is holding it.

One more time, and then I will stop asking: **type the fact table.**

— Sir JB
