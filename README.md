# BDAT04 — Data Warehousing for Business
### Lyceum of the Philippines University – Laguna · College of Business Administration
### BS Business Administration major in Business Data Analytics · Term 1, AY 2026–2027

**Repository:** https://github.com/JBBongalos-LPU/BDAT04-2026_T1 (private)

This repository is where every graded deliverable in this course lives. Treat it as your working file cabinet, not an afterthought at the end of a milestone.

**Course facilitator:** Jerald B. Bongalos — jerald.bongalos@lpulaguna.edu.ph
**Class:** Saturdays, 9:00 AM, online via Microsoft Teams
**Consultation hours:** _[to be agreed and written here]_

---

## The class

| Student | Folder | Case | Functional page | Named reader |
|---|---|---|---|---|
| Lopez, Val Anthonne C. | `anthonne-lopez/` | **P4** | Sales & Customer Performance | Sales Manager |
| Sanchez, Eliah Therrien Estrella | `eliah-sanchez/` | **P5** | Profitability | CFO |
| Alcantara, Angus Jullian G. | `angus-alcantara/` | **P6** | Workforce | HR Director |
| Lagdamen, Lawrence | `lawrence-lagdamen/` | **P7** | Operations | Operations Manager |

Everyone builds the complete warehouse and all four report pages. Your assigned case is the page you deep-dive, present and defend.

---

## The data

The integrated business case is **Kape Tayo Coffee** — a six-branch chain in Laguna, January 2025 to June 2026. Seven source files, roughly 12,000 rows.

📁 **Download:** https://drive.google.com/drive/folders/1Z8bcT8oyLXgakBUK0vC_OYw39g2KU2rn

Do **not** commit the raw source files to this repository. Everyone works from the same Drive copy so that nobody is silently building on a version they edited.

The same case continues into **BDAT05 Fundamentals of Predictive Analytics** — the warehouse you build here is the data foundation you will model on there.

---

## How to submit

You do not need to install anything. Everything is done through the GitHub website.

1. Open your folder, then the sub-folder for the milestone
2. **Add file → Upload files**
3. Drag your document in
4. Write one line in the commit box describing what you uploaded
5. **Commit changes**

That one-line commit message is your audit trail. "B1 draft — parts A and C done, verdict pending" is useful. "update" is not.

---

## Folder structure

```
your-name/
  b1-inventory/            Source inventory and data quality assessment
  b2-cleaned-dataset/      Cleaned, documented queries
  b3-model-design/         Grain statements and schema design
  b4-star-schema/          Validated model
  b5-measure-library/      Core DAX measures
  b6-time-intelligence/    Period-over-period measures
  b7-report-pages/         The four functional report pages
  b8-published-and-docs/   Published dashboard and documentation pack
  backups/                 Exports and dated snapshots
  ai-use-log.md            Running log — one entry per milestone
```

---

## Milestones

Dates follow the current Saturday calendar and will be confirmed in class.

| Code | Milestone | Due |
|---|---|---|
| **B1** | Data Source Inventory and Quality Assessment | **Mon 24 Aug 2026, 11:59 PM** (extended, no penalty) |
| B2 | Cleaned and Documented Dataset | Week 4 — 5 Sep |
| B3 | Dimensional Model Design | Week 6 — 19 Sep |
| B4 | Star Schema Build | Week 7 — 26 Sep |
| B5 | Measure Library | Week 8 — 3 Oct |
| B6 | Time Intelligence Measure Set | Week 10 — 17 Oct |
| B7 | Four Functional Report Pages | Week 11 — 24 Oct |
| B8 | Published Dashboard and Documentation Pack | Weeks 12–13A — 31 Oct / 7 Nov |

Late laboratory work and milestones: −10% per calendar day to a maximum of three days, after which the work is recorded as not submitted but must still be completed, because the next milestone depends on it.

---

## The five gates

These are pass-or-fail. Failing any one caps the course grade at the passing threshold regardless of points, because each is a professional standard rather than a scale of quality.

1. **Refreshability** — your model must refresh end to end from the source files without manual repair
2. **Declared grain** — no fact table without a written statement in the form "one row represents …"
3. **Lawful data** — no personal data without a documented lawful basis; nothing confidential uploaded to a public AI service
4. **Honest visuals** — no truncated axes, mismatched dual scales, or charts that overstate; limitations stated on the dashboard itself
5. **Authorship** — you can explain, orally and without notes, any step, relationship or measure you submit

---

## AI use

Generative AI is a legitimate professional tool and this course teaches its use. It is governed by tier, and by one overriding rule: **you are accountable for everything you submit, including any error the tool introduced.**

| Tier | Status |
|---|---|
| 1 | Permitted, no disclosure — grammar, translation, looking up what a function does |
| 2 | Permitted **with disclosure** in your AI Use Log — explaining an error, suggesting an approach, reviewing something you wrote |
| 3 | **Prior written approval** — AI-generated DAX or M that materially produces a submitted query or measure |
| 4 | **Prohibited** — passing off AI interpretation as your own reasoning; AI during assessment or defense; uploading real personal data to a public AI service |

Every graded milestone carries an entry in your `ai-use-log.md`. An honest log is never penalised. An absent or false one is.

---

## Ground rules

- **Never edit the source data.** Altering source data to produce a more attractive result is data fabrication, the gravest offence in this course, and is referred directly to the institutional disciplinary process.
- **Do not commit other people's work.** Your folder is yours.
- **File loss is not an accepted excuse.** This repository, plus Power BI's own version history, is your backup.
- **Ask early.** A question on Sunday is worth more than an explanation on Tuesday.
