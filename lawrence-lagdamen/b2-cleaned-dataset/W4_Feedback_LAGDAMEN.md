# B2 — Cleaned and Documented Dataset · Week 4 Feedback

**Lawrence Lagdamen** · Case P7 — Operations
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027

---

## Your mark: 76 / 100

> The best analytical work anyone has produced in this course. Submitted inside a model that still has the workings in it.

| Criterion | Score | Weight |
|---|---|---|
| Technical correctness | 2.5 / 4 | 35% |
| Business justification | **4 / 4** | 25% |
| Documentation and readability | 3 / 4 | 20% |
| Response to prior feedback | 2.5 / 4 | 15% |
| Timeliness and integrity | **4 / 4** | 5% |

**Read the whole letter before you look at that number again.** Two of those scores are the highest in the class, and the mark moved for one reason only.

---

## Your integrity report is the best student work this course has produced

I mean that without qualification. I checked every figure in it against the source file. **They are all correct**, including one that nobody else in the class found and that I had not put there on purpose.

### The customer relationship

You reported:

> **5,047 rows returned** — 5,039 null CustomerIDs plus **8 true non-null orphan rows** using `C0182`, `C0183`, and `C0184`.

I verified this. `tblCustomers` holds 186 records, but the IDs are **not** a contiguous run — they stop looking sequential partway through, so `C0182` is not simply "the 182nd customer." Those three IDs genuinely do not exist. They arrived with the July file. There are exactly eight such rows.

Everyone else in the class reported this relationship as either "null" or **zero**. You are the only person who took a 5,047-row anti-join result and asked whether all 5,047 were the same kind of problem. They were not.

**That is the entire lesson of the week, executed at a level I did not teach.** The session taught you that blanks and orphans are different things. You applied it *inside a single result set* and separated them.

### And the rest of it

**Sales → Branches in two stages.** 66 unmatched → apply the recognisable fixes → 26 remain → all `B07` → ACCEPT. You did not report one number; you reported what happened to the number as you worked. That is how a finding gets written up.

**You separated the null date from the 40 distinct unmatched dates** in the calendar check — the same discipline again, unprompted.

**You named the employee.** `E004`, Bea Ramos, branch `B07`. Not "1 orphan row." A person, at a branch, which a manager could act on this afternoon.

**And you closed your own loop from Week 3:** *"Retained `QuantityMoved = -15` — confirmed as a valid Transfer Out that happened only once, not an error."* That was the false positive your own improvised method threw up last week. You went back and settled it.

Your AI Use Log is also the best in the class — five entries, each naming what you verified.

---

## Where the mark went

Your transformation notes end with this:

> *"Temporary investigation steps such as diagnostic filters, Remove Duplicates used only to identify distinct offending values, Group By steps, and other scratch-work steps were removed after their results were recorded. The final model keeps the cleaning decisions, not the investigation process."*

That paragraph is correct as a principle and it is the right thing to have written. **But your submitted model does not do it.**

```
table Merge          →  Table.NestedJoin(tblSales, {"BranchID"}, tblBranches, …, JoinKind.LeftAnti)
table 'Merge (2)'    →  Table.NestedJoin(tblSales, {"ProductID"}, …, JoinKind.LeftAnti)
table 'Merge (3)'    →  Table.NestedJoin(tblSales, {"Date"}, …, JoinKind.LeftAnti)
table 'Merge (4)'    →  Table.NestedJoin(tblSales, {"CustomerID"}, …, JoinKind.LeftAnti)
table 'Merge (5)'    →  Table.NestedJoin(tblInventory, {"Date"}, …, JoinKind.LeftAnti)
table 'Merge (6)'    →  Table.NestedJoin(tblEmployees, {"BranchID"}, …, JoinKind.LeftAnti)
```

**All six diagnostics are still loaded as tables**, under default names. Your model now contains six phantom tables that are not part of the warehouse — they are the questions you asked on the way to the answers.

This is the same fault as Week 3, wearing different clothes. Last week you left investigation *steps* inside two tables and reduced `tblSales` to 23 rows. This week the tables are intact — you rebuilt them properly, which I do credit — but the investigations moved out and became six queries of their own, and they were never unloaded.

It matters more than it looks. In Week 6 you will build a star schema and Power BI will offer you relationships between every table in the model. Six near-duplicates of `tblSales` sitting there will produce a diagram nobody can read and ambiguity the engine resolves by guessing.

**The fix is one right-click.** In Power Query, right-click each `Merge` query → untick **Enable load**. The query stays, so your working is preserved and auditable. It just stops being a table in the model. That is the professional answer: keep the investigation, don't ship it.

### Two smaller things

**No `SourcePath` parameter.** Section 5 of the laboratory sheet, and every one of your queries still carries the full literal path — including `KapeTayo_IntegratedCase 1.xlsx`, with a duplicate-download suffix. Your July file points at a different folder again. Three of your classmates now have a parameter; you have eight hard-coded URLs.

**`Quantity` and `Amount` are still text** in `tblSales`. `UnitPrice` you typed. The other two you did not, and they are the two that have to add up.

**Naming is half-done.** `FIX - Trim BranchID`, `FIX - Uppercase BranchID`, `FIX - Standardize BranchID` are excellent — the prefix tells a reader it was a decision, not a repair. But `Added custom`, `Removed columns` and `Appended query` sit in the same list. You know what good looks like; apply it to all of them.

---

## Where to push next

- **Untick Enable load on all six Merge queries.** One right-click each. Do it before Week 6.
- **Add the `SourcePath` parameter** and re-point all eight queries.
- **Type `Quantity` and `Amount`.**
- **Finish naming your steps** to the standard your own `FIX -` prefix already sets.

---

## Closing

Here is your arc, and it needs saying plainly.

**B1 81 · Week 3 79 · B2 76.** Three milestones, sliding — while producing, each time, the sharpest analysis in the room. That is a frustrating pattern and I would rather name it than let you work it out from the numbers.

It is not your thinking. Your thinking has been the strongest in this class since Week 2 and it improved again this week. The integrity report you submitted is the piece of work I will keep as the example for next year's cohort, with your name on it if you allow me.

What is sliding is the gap between **doing the work** and **handing in the work**. In B1 the analysis was better than the report. In Week 3 the investigation was better than the model. This week the report is outstanding and the model still carries the scaffolding — and the notes say the scaffolding is gone, which means the two halves of your submission disagree.

An analyst who finds what nobody else finds and hands in a file the next person cannot use has done half a job. You are doing the difficult half brilliantly and losing marks on the half I could teach anyone in ten minutes.

**Untick six boxes, add one parameter, type two columns.** That is the entire distance between 76 and a mark that reflects what you actually did.

And on Saturday, when you sit the prelim: the reasoning you showed in that report — *5,047 is not one number, it is 5,039 and 8* — is exactly what the practical component rewards. Take it in with you.

— Sir JB
