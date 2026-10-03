# BDAT04 Midterm Assessment — complete pack

**Saturday 3 October 2026 · 100 points + 3 bonus · Rubric B (re-weighted)**
Fundamentals of Data Warehousing · Term 1, AY 2026–2027 · LPU–Laguna

---

## What is in this zip

```
01_STUDENT/       given to students
02_DATASET/       upload to Drive, release at Test II start
03_INSTRUCTOR/    your copies — do not distribute
04_SOURCE/        generators, so anything here can be rebuilt or re-measured
```

---

## The exam

| | | Time | Points |
|---|---|---|---|
| **TEST I** | Written examination — three situational essays | 90 min | **50** |
| **TEST II** | Practical demonstration — four drawn tasks, Bands A–D | 120 min | **45** |
| **TEST III** | Oral interpretation | ~5 min each | **5** |
| **TEST IV** | Bonus card — modelling vocabulary | ~3 min each | **+3** |

**Conditions.** Open notes for Tests I and II — syllabus, the three advance reading packets, feedback letters, laboratory and activity sheets, and their own Power BI model. **No AI tools of any kind.** Test III is closed-book.

**Coverage: Weeks 1–6**, including all three advance readings — W3 (types, applied steps, the Service's missing profiling panes), W4 (join kinds, append-by-name, ETL vs ELT, referential integrity), S6 (grain, facts and dimensions, conformed dimensions, cardinality).

---

## Two changes from the syllabus, both deliberate

**1 · Rubric B re-weighted.** The printed rubric gives 25% to DAX measures. DAX is Week 8 content and the midterm moved to Week 7, so it has not been taught. That 25% is redistributed into the two criteria Sessions 5B and 6 actually delivered:

| Criterion | Printed | This midterm |
|---|:--:|:--:|
| Data preparation | 15 | **15** |
| Grain and dimensional design | 30 | **45** |
| Relationships and model validation | 25 | **35** |
| DAX measures | 25 | **deferred to the final** |
| Interpretation | 5 | **5** |

**2 · Midterm Grade = Midterm Assessment 50% + milestone B3 50%.** The syllabus formula needs B3, B4 and B5. Only B3 exists on 3 October; B4 and B5 move into the final grade computation.

**Both belong in the syllabus amendment memo to the Dean. That memo is not yet written.**

---

## Running the day

1. **Setup** — draw slips for Bands A, B, C, D; hand out Test I notebook link and Test II task sheets.
2. **Test I, 90 minutes.** Notebook downloaded from the LMS, opened in their own Colab. Draft collected in the room.
3. **Break.**
4. **Test II, 120 minutes.** Release the dataset links at the start, not before. Take the TMDL export in the last ten minutes.
5. **Test III and IV.** Oral, then one bonus card drawn blind.

**Post-examination:** polished essay version and prompt log with conversation link due **Sunday 4 October, 11:59 PM**, into `midterm-assessment/` in the class repository.

---

## The dataset — Bayanihan Bus Lines

A Laguna–Quezon provincial bus operator. Unseen by the students. Shaped for **modelling**, not cleaning.

**Three fact tables at three different grains** — the point of the whole exam:

| Table | Rows | Grain |
|---|---:|---|
| `Tickets` | 18,329 | one ticket sold |
| `Trips` | 1,200 | one trip departure |
| `Maintenance` | 260 | one maintenance job |

Tickets per trip run 6 to 26, mean 15.26. A trip is not a ticket.

**Dimensions:** Routes (12) · Buses (18) · Crew (40) · Calendar (546 days, 2025-01-01 → 2026-06-30).
**Conformed:** Calendar serves all three facts · Routes serves two · Buses serves two.

### Planted, and measured from the delivered files

| Defect | Measured |
|---|---|
| Duplicate ticket rows | 18,329 → **18,298**; 31 surplus worth **₱4,947.53** |
| `OdometerKM` is text | **19** comma values; repaired range 48,000–611,741 |
| Dirty `RouteID` | 16 raw distinct → **12**; **27 rows** (`r01` 9 · `R-02` 7 · `R03␣` 6 · `r07` 5) |
| Blank dates in Trips | **6** |
| Trips → Buses orphans | **17** (`BU099`) |
| Tickets → Trips orphans | **23** (`T99999`) |
| Crew never scheduled | **6 — all of them Inspectors** |
| Charter trips | **14** beyond the fuel fence of 130.70 L, max 504.1 L — legitimate |

Revenue: **₱2,528,647.94** raw · **₱2,523,700.41** deduped.

### The three judgment cases

1. **Maintenance** — fact or dimension? It is a fact, at a third grain. Size is not the test.
2. **Six Inspectors nobody scheduled** — an entire role with no fact table recording it.
3. **Tickets carries `TripID`** — should you join fact to fact? The hardest item in the pool.

---

## Known caveats

- **The prelim was never returned.** No "response to prior feedback" criterion appears anywhere in this marking, because it could not be assessed fairly.
- **Test II's B2 has no surviving orphan route.** All 27 dirty rows repair. This differs from the prelim's branch task on purpose — a student who reports a leftover unknown route has mis-repaired.
- **Bands are drawn, not assigned.** Prepare slips before the session.

---

## Rebuilding anything

```bash
python3 04_SOURCE/build_bayanihan.py   # regenerates the seven data files (seed 1003)
python3 04_SOURCE/measure.py           # re-measures every figure quoted above
python3 04_SOURCE/build_notebook.py    # rebuilds the Test I notebook
python3 04_SOURCE/build_pack.py        # rebuilds sheets, key, cards, scoring sheet
```

The seed is fixed, so a rebuild reproduces the same data and the same answer key.

**— prepared for Jerald B. Bongalos**
