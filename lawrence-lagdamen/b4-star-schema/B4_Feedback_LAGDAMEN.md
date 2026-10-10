# B4 — Star Schema Build

**Lawrence M. Lagdamen** · Case P7 — Operations
BDAT04 Fundamentals of Data Warehousing · Term 1, AY 2026–2027
Session 7, asynchronous · marked 10 October 2026

---

## Mark: 65.0 / 100

*The cleanest model in the class, carrying the thinnest paperwork in the class.*

---

## Rubric D

| Criterion | Weight | Level | Why |
|---|:--:|:--:|---|
| Technical correctness | 35 | 3 | `dimDate` complete and correct, `tblCalendar` properly disconnected, validation exact. One relationship missing and one orphan comparison misstated. |
| Business justification | 25 | 3 | Grain statements sound and the Item 1 reflection is genuinely good. The filter-direction answer is circular, and the `List.Dates` explanation never arrived. |
| Documentation and readability | 20 | **2** | Screenshots unreadable at 625 px, filename doubled, no TMDL export. |
| Response to prior feedback | 15 | **2** | The TMDL was the one named item in your last letter. It did not come. |
| Timeliness and integrity | 5 | **2** | No AI Use Log entry for B4, which is required even when the answer is "none used". |

Σ(level × weight) ÷ 4 = **65.0**

---

## What you did well

Lawrence, I want to start with something I can only say about you: **your `dimDate` is the only complete one in this class.** Date, Day, Day of week, Month, Month name, Quarter, Year — every column Item 5.3 asked for, all there. Three other people built that table and you are the only one who finished it. When we get to Week 10 and start writing year-to-date and same-period-last-year, you will already be standing on the foundation and they will be going back to build it.

Your model is the cleanest of the four. `tblCalendar` is properly disconnected rather than left wired to nothing in particular. The July data is appended and the source query is tidied away — Alcantara still has `tblSalesJul2026` floating in his model view; you do not. Your validation total is exact at ₱2,694,600.80.

And your Item 1 reflection is a real answer: you worked out that Power BI declining to join `tblSales` and `tblInventory` on `BranchID` is *correct*, because both tables hold many rows per branch and joining them would multiply rows and produce inflated figures. That is exactly right, and most students at this level do not see it.

---

## Where the marks went, and it is not the model

Everything I had to deduct sits around the work rather than inside it.

**The TMDL export did not come.** Lawrence — this was the one named item in your last letter. I wrote that it was the cheapest mark in the course and that you had left it on the table. It is the entire basis of *Response to prior feedback*, which is fifteen percent of this mark, and there was nothing to score. Teyen submitted two TMDLs, including a pre-activity backup nobody asked twice for. You submitted none.

**Your screenshots are 625 by 530 pixels.** I cannot read a single column name in them. The model view *is* the evidence for Item 6 — it is how I check that your relationships are what your table says they are — and at that size it evidences nothing. Full window, every time.

**No AI Use Log entry for B4.** Required even when the honest answer is "No AI use." It takes one line.

**Your file is named `B4_Star_Schema_Lagdamen.docx.docx`.**

**You never explained the three arguments of `List.Dates`.** The sheet asks for it explicitly and marks it. You wrote that the query "includes all the aforementioned columns needed" — which is true, and is not the question.

**One factual slip worth naming.** You report `tblSales → tblBranches` as 26, "same as Week 4." Week 4 was **66** — forty formatting variants plus twenty-six `B07`. Your 26 is very likely right *after* your own cleaning removed the variants, and that is a good result. But "same as Week 4" is not, and the sentence as written tells me you did not look the number up. Verify against the record, not against memory.

**`tblEmployees → tblBranches` is missing** from your relationship table.

---

## What I am actually asking you

This is the same shape as the midterm, where you left the written paper after a third of the time and your practical was the best in the room. I said then that it was not an ability problem. It still is not. But the pattern has now cost you marks three times, and a model nobody can verify is worth less than a worse model somebody can.

**Before B5, do these three things once and they become habits:** export the TMDL before you close the browser, screenshot at full window, write the AI log line while you work. Fifteen minutes total, across the whole milestone. On this mark that fifteen minutes was worth about twenty points.

B5 is DAX measures and filter context, due noon Friday 16 October. Your hands will carry the measures. Read the AI rule on page 1 before you start — it concerns Copilot, and it is not optional.

---

You built the best model in this class and told me the least about it. I would like, once, to read a sheet as good as your schema.

**Export the TMDL before you close the tab. That is the whole ask.**

*Jerald B. Bongalos · Course Facilitator, BDAT04 · College of Business and Accountancy, LPU – Laguna*
