# Week 3 Asynchronous Activity — Feedback

**Lawrence Lagdamen** · Case P7 — Operations
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027

---

## Your mark: 79 / 100

> The best reasoning in the class, again. This time you also left the scaffolding standing inside the building.

| Criterion | Score | Weight |
|---|---|---|
| Technical correctness | 2.5 / 4 | 35% |
| Business justification | 4 / 4 | 25% |
| Documentation and readability | 2.5 / 4 | 20% |
| Response to prior feedback | 4 / 4 | 15% |
| Timeliness and integrity | 4 / 4 | 5% |

**Business justification 4/4 is the highest single score I have given anyone this week.** Read on before you look at the total.

---

## What you did well

### You solved a problem I could not

Part B2 told you the conversion would produce errors. On your machine it produced none — my instruction was wrong for your regional settings, and I only worked that out afterwards.

Everyone else stopped there. You did this instead:

```m
#"Grouped rows" = Table.Group(#"Changed column type", {"QuantityMoved"},
                     {{"Count", each Table.RowCount(_), Int64.Type}}),
#"Filtered rows" = Table.SelectRows(#"Grouped rows", each ([Count] = 1))
```

You grouped the column by value, counted each one, and kept only the values appearing exactly once — reasoning that the corrupted bulk figures would be large and unique while ordinary quantities repeat. **That works.** You found the fourteen, you correctly identified them as *"numbers containing thousands,"* and you diagnosed the cause: *"the values containing commas as thousand separators caused the error."*

I checked what your method actually returns. It surfaces **fifteen** candidates — the fourteen comma-formatted deliveries plus one ordinary Transfer Out of −15 that happens to occur only once. You reported fourteen. So you did not just run the query; you looked at the fifteen rows it gave you and correctly threw out the false positive.

When the prescribed method failed, you built a working one from the technique you had been taught two days earlier and then validated its output. That is the most impressive single thing anyone did this week — and I want you to present it yourself on Saturday. Details at the end of this letter.

### Your answer on the blank customer IDs is the model answer

You classified it correctly — walk-in customers, not a defect — refused to delete, and then went one step further than anyone: *"I would document that a 'null' CustomerID represents walk-in transactions."*

That is exactly right. The fix is not to fill the field. It is to write down what its absence means, so that every report built afterwards inherits the meaning instead of rediscovering it.

Your reflection makes the reasoning concrete with the SMAC comparison — not everyone at SM is registered. That is the correct instinct: when a field is empty for nearly half your rows, ask whether it is *missing* or whether it was never *applicable*.

### Part A3 — you were the only one who answered both halves

I asked what the first number answers and what the second answers. You gave me both, separately, and then chose the right one to report. Everyone else told me which they would report and skipped the distinction. **46 is how many rows are involved. 23 is how many to remove.** You had that straight.

### Part B3 — the most disciplined answer in the class

> *"From this calculation alone, I will not be able to determine which of these rows are incorrect. Overwriting these values without any additional evidence is not ideal. I would tell the branch manager that 23 transactions have Amount values that do not reconcile with Quantity × UnitPrice and ask that they be checked against the original transaction records before making any corrections."*

You refused to guess. Another student found the same 23 rows and attached a theory to them — loyalty discounts — which turns out to explain fewer than half of them. You declined to explain what you could not yet support, and asked for the source records instead. That is the answer a working analyst gives.

### You did exactly what your B1 feedback asked

B1 said: *count everything you find; never write "some" where a number belongs; fill in every field the brief asks for.*

Every number in this submission is present and correct. Every field is filled. You added screenshots nobody asked for. Your B1 mark was your analysis reported at a lower standard than it deserved — that gap has closed.

Your AI Use Log fixed **both** things I asked for: the Tier column is filled, and you wrote one entry per distinct use rather than one for the whole milestone. Three entries, each with what you verified. That is the standard.

And you were honest in your reflection that the interface confuses you and that AI helped you finish. That is precisely what the policy is for. Nothing in your log is anything but permitted, disclosed use, and saying so plainly is worth more than pretending otherwise.

---

## Where the marks went

You left your investigation steps inside the model. Both of your main tables are now the *result of a query experiment* rather than the data.

**`tblSales` now contains 23 rows.**

```m
#"Column for checking" = Table.AddColumn(#"Changed Date", "Check", each [Quantity]*[UnitPrice]-[Amount]),
// This showed how many irrelevant data are present in the data set.
#"Error checking" = Table.SelectRows(#"Column for checking", each [Check] <> 0)
```

That last step filters your fact table down to only the mismatched rows. Ten thousand five hundred and sixty-six sales are gone from your model. Everything downstream — revenue, branch comparison, product performance — would now be computed from 23 broken transactions.

**`tblInventory` now contains 15 rows and 2 columns.** The Group By and the Count = 1 filter are still there, so `MovementID`, `Date`, `BranchID`, `ProductID` and `MovementType` no longer exist in your model.

The activity said it in Part A: *then remove the step and move on.* Counting changes your query. A count is something you **read** and then undo — it is not something you keep.

This is a mechanical mistake, not a thinking one. But it is a serious one, because a model in this state produces confident wrong answers rather than obvious errors.

**Three smaller things in the same family:**

- Your reflection says the duplicates were removed and the table went to 10,566 rows. **Your model never removes them** — there is no `Table.Distinct` step anywhere. You did it, read the number, and undid it. The reflection describes work the model does not contain.
- `tblCustomers` has no type step at all, so `JoinedDate` is still text and will not join to your calendar.
- In `tblSales`, `UnitPrice` and `Check` are still text while `Quantity` and `Amount` are numbers.

**And one wording point worth catching.** Your comment reads *"This showed how many irrelevant data are present in the data set."* But your own Part B3 answer says — correctly — that you cannot yet determine which of those rows are wrong. They are not irrelevant. They are **unreconciled**, which is a different and more careful word. Your comment contradicts your best paragraph. Make the comment say what the analysis says.

---

## Where to push next

- **Undo every counting step before you close the editor.** Read the number, write it down, delete the step. Your model should end the session containing your *decisions*, not your *investigations*.

- **Rebuild `tblSales` and `tblInventory`.** Remove the filter steps, then re-apply only the changes you actually decided on: remove the 23 duplicates, set the date type, type `UnitPrice`. Keep the `Check` column if you like — it is genuinely useful — but do not filter on it.

- **Finish naming your steps.** `Changed Date`, `Column for checking` and `Error checking` are yours and they read well. `Changed column type`, `Grouped rows` and `Filtered rows` are still the machine talking. You are most of the way there.

- **Answer the fourth reflection question.** What did you find this week that you missed completely in B1? You skipped it, and it is the one that measures whether the week landed.

---

## Closing

In your B1 letter I wrote that you are the best analyst in this class and your mark does not say so — and that the gap was reporting, not thinking.

**The reporting gap is closed.** Every number counted, every field filled, screenshots supplied, AI log corrected in both the ways I asked. Business justification at 4 out of 4 and response to prior feedback at 4 out of 4 are the two highest scores on this activity in the class. You did the work I asked you to do and it shows immediately.

What happened instead is new, and smaller, and entirely fixable: you left your workings on the page. You investigated brilliantly — genuinely, the B2 improvisation is better than the exercise I wrote — and then handed in the investigation instead of the conclusion.

Think of it as the difference between a working sheet and a report. Everything you did was right. It just needed to be cleared away before you submitted, the way you would delete the scratch calculations from the margin before handing in the paper.

**Rebuild the two tables and send me the corrected TMDL by Saturday.** I will not re-mark this, but I want to see the model in the state your own analysis deserves — and you should have one you can actually build on in Week 4, because we start using these tables in anger next week.

---

## On Saturday — you are walking us through your work

I am giving you the floor for about ten minutes at the start of the session. Not a presentation. Your laptop on the projector, your query open, talking us through what you actually did.

**What I want you to cover:**

1. **What the sheet told you would happen in B2, and what actually happened.** Say plainly that you got no errors and that the instruction was wrong for your machine.
2. **What you did next.** Walk through the Group By, the Count column, and the filter to Count = 1 — clicking through it live, not describing it.
3. **Why you expected that to work.** The reasoning is the valuable part: corrupted bulk figures are large and unique; ordinary quantities repeat. Say it in your own words.
4. **The fifteenth row.** Your method returned fifteen candidates and you reported fourteen. Tell them how you decided the −15 did not belong. That is the step most people would have skipped.

**What you do not need to do:** rehearse, use slides, or sound polished. If you get lost in the interface mid-demo, say so and keep going — the class needs to see that too, and you will not be the only one who has been lost this week.

You told me in your reflection that Power BI is new to you and that most of the functions confuse you. That is exactly why this is worth ten minutes of everyone's time. The person who worked around a broken instruction is not the person who has mastered the tool — it is the person who kept thinking when the tool stopped cooperating. Your classmates need to hear that from you rather than from me.

Come and find me before we start if you would rather run through it once first. And if you would genuinely rather not do this, tell me before Saturday and I will present it with your name on it instead — but I would rather it came from you.

---

One more thing. You told me the interface confuses you. Reading what you produced, that confusion is costing you nothing at all — you worked around a broken instruction by inventing a method I had not taught you. The tool will get familiar. The thinking is the part that is hard to teach, and you already have it.

— Sir JB
