# Week 3 Asynchronous Activity — Feedback

**Angus Jullian G. Alcantara** · Case P6 — Workforce
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027

---

## Your mark: 83 / 100

> Every measurement correct. One conclusion that the evidence does not support.

| Criterion | Score | Weight |
|---|---|---|
| Technical correctness | 3 / 4 | 35% |
| Business justification | 3 / 4 | 25% |
| Documentation and readability | 4 / 4 | 20% |
| Response to prior feedback | 3.5 / 4 | 15% |
| Timeliness and integrity | 4 / 4 | 5% |

*Same mark as B1, but a different shape. B1 was won on completeness. This one is won on documentation and lost, slightly, on reading the evidence.*

---

## What you did well

**Every number in your sheet is right. All of them.** MovementType 5, Tier 5, PaymentMethod 3, Category 5, 4,775 blank customer IDs at 45.09%, 46 duplicate rows and 23 surplus, 10,566 remaining, 12 blank dates, 23 amount mismatches. I checked each against the source file. There is not one arithmetic error in the submission.

**Your predictions are real, and I can tell.** You guessed 11 for Product Category and the answer was 5. You left it there. It would have taken five seconds to change an 11 to a 5 and nobody would ever have known — and the whole exercise would have been worthless. You also predicted 50% for blank customer IDs against an actual 45.09%, close enough that I believe you reasoned it rather than guessed. That is the part of this activity I actually cared about.

**The inventory work is the best thing in the submission.**

```m
#"Replacing value or removing the comma" =
    Table.ReplaceValue(..., ",", "", ..., {"QuantityMoved"}),
#"Converted QuantityMoved to Whole numbers" =
    Table.TransformColumnTypes(..., {{"QuantityMoved", Int64.Type}})
```

Replace first, then convert. That is the correct order, and you did it **even though your machine gave you no error to fix**. Your comment explains why — so the query will not break for someone whose regional settings differ from yours. You reached the right conclusion from an experiment that failed to produce the evidence it was supposed to. That is harder than the exercise I actually set.

**Your applied steps are documentation now.** *Removed 23 duplicate SaleIDs*, *Set Date column to Date Type*, *Added Check column to verify Account*. A stranger can read that list and follow what you did.

And you went further than I asked. I asked for step *descriptions*; you wrote M comments in the query itself. Those are better, and here is why: descriptions can be lost when a model is exported or rebuilt. Comments live inside the code and travel with it. You found a more durable answer than the one on the sheet.

**You refused to overwrite the Amount column.** Twenty-three rows disagreed with your arithmetic and you left every one of them alone and reported them instead. That single decision is the whole of Part B3, and most people fail it by being helpful.

---

## Part by part

### Part A

Complete and correct. You named both impostors in Tier (`REG` and `silver`) and the single one in MovementType (`delivery`), and you correctly called PaymentMethod and Category **clean** rather than inventing problems in them. Proving a column is fine is a real finding, and only counting can do it.

Your answer on the blank customer IDs goes past what I asked. You said it is how the business works, not a defect — correct — and then added that you would give those rows a category of their own. That is what a working analyst does: a walk-in bucket, so the 45% stays visible in every report instead of silently vanishing from customer analysis. Nobody else proposed that.

### Part B1

12 blank dates. Correct.

### Part B2

You hit the locale problem and handled it honestly, both in your answer and in your reflection. Two small things:

1. Your sheet says *"Errors found: 14"* but you observed none. Write down what you saw, not what was expected — even when the expected answer is printed on the last page.
2. I asked which of the two sequences works, and you described what happened instead of naming it. Your query proves you know the answer; say it anyway.

**The question you did not answer:** if you had clicked Remove Errors, which rows would you have lost, and what do they have in common? Go and look. All fourteen are the same movement type, and they are the largest quantities in the table. That is not a coincidence, and it is worth understanding before Week 6.

### Part B3 — where the mark moved

You wrote that the 23 rows are all cases where *"the Amount paid is lower than the expected Amount value,"* and attributed them to loyalty discounts.

> **Of the 23: eleven are lower. Twelve are higher.**
>
> A discount cannot make a customer pay more than quantity × price. Several of those rows are −600.00, −420.00, −310.00 — the customer was charged hundreds of pesos above the arithmetic. Your discount theory explains fewer than half your findings, and the other half point at something else entirely.

You did the hard part right and stopped one step early. You built the Check column, you counted it, and you refused to overwrite the data. Then you explained the result instead of examining it. Sorting that column by value — biggest to smallest — would have taken one click and shown you the negatives immediately.

**The habit to build:** after you produce a number, look at the rows behind it before you write the sentence that explains them. A count tells you how many. It does not tell you what they are.

### Parts C and D

Full credit. Seven tables exported cleanly, steps named, reasoning embedded. Your backup is genuinely restorable, which is the only test that matters.

---

## Where to push next

- **Type your fact table.** In `tblSales`, `Quantity`, `UnitPrice`, `Amount` and `Check` are all still text. Compare `tblProducts`, where `ListPrice` is a whole number that sums. Your model cannot currently total your own revenue column — and revenue is the number the entire warehouse exists to produce. This is Part B's lesson landing in the one table where it costs the most.

- **Check what happened to `YearMonth`.** In the source it is the text `2025-01`. Your model has it as a date. Open it and see what it now contains — a month label may have quietly become a specific day. Same class of problem as the commas, opposite direction.

- **Answer the fourth reflection question.** What did you find this week that you missed completely in B1? That question is the point of the whole week, and it is the one you skipped.

- **You still owe me the emails.** In your B1 feedback I asked you to look again at the six customer emails written in uppercase and work out what they were the fingerprint of. That is still open.

---

## Closing

Eighty-three in B1, eighty-three here, and they were earned differently. B1 was the most complete submission in the class. This one is the best-documented — your query now reads like something a colleague could inherit, which is a professional standard, not a student one.

The thing standing between you and a higher mark is not a skill you lack. You can count, you can type data correctly, you can document, and you have the judgement to leave suspicious data alone rather than tidying it away. What happened in B3 is that you found something genuinely interesting and then reached for the first explanation that fit, instead of testing whether it fit *all* of it. Eleven rows agreed with you and twelve did not.

**That is a good problem to have, because it is a habit rather than a gap, and habits change quickly once you have seen them.** Next time you write a sentence beginning *"I found 23 transactions where…"*, stop and go look at all 23 first.

**Bring the negative rows to Saturday.** I want you to tell the class what you think is going on in them — I have my own theory, and I would rather hear yours first.

— Sir JB
