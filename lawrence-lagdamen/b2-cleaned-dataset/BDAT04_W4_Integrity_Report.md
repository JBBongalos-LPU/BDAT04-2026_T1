# BDAT04 Week 4 — Integrity Report

## Six required Left Anti relationships

| Relationship | Join key | Initial Left Anti result | Distinct offending values / finding | Decision |
|---|---|---:|---|---|
| `tblSales → tblBranches` | `BranchID` | 66 rows | `b01`, `b04`, `B-02`, `B-05`, malformed `B03`, malformed `B06`, and `B07` | **FIX** recognizable formatting issues; after the fixes, 26 rows remained and all were `B07` → **ACCEPT** |
| `tblSales → tblProducts` | `ProductID` | 9 rows | `P99` | **ESCALATE** |
| `tblSales → tblCalendar` | `Date` | 771 rows returned | 40 distinct non-null unmatched dates plus 1 null Date value | Retain the non-null source records; treat the null Date separately as a blank |
| `tblSales → tblCustomers` | `CustomerID` | 5,047 rows returned | 5,039 null CustomerIDs plus 8 true non-null orphan rows using `C0182`, `C0183`, and `C0184` | Nulls are blanks, not orphans; **ESCALATE** the 8 true orphan rows |
| `tblInventory → tblCalendar` | `Date` | 82 rows | `1/15/2025`, `9/1/2025` | Retain the source records; the dates are missing from the calendar reference |
| `tblEmployees → tblBranches` | `BranchID` | 1 row | `B07` — Employee `E004`, Bea Ramos | **ACCEPT** |

## Sales → Branches detail

Initial Left Anti result: **66 unmatched rows**

Recognizable formatting issues were identified and fixed:

- `b01` → `B01`
- `b04` → `B04`
- `B-02` → `B02`
- `B-05` → `B05`
- malformed `B03` → `B03`
- malformed `B06` → `B06`

After the FIX steps, the Left Anti result fell from **66 rows to 26 rows**.

All 26 remaining rows use:

- `BranchID = B07`

Decision: **ACCEPT B07**, because the activity states that B07 opened in July. The sales values are real; `tblBranches` is incomplete.

## Sales → Products detail

Initial and final diagnostic result:

- **9 orphan rows**
- Distinct offending ProductID: `P99`

Decision: **ESCALATE**

`P99` does not exist in `tblProducts`, and there is not enough evidence to determine which valid product should replace it without inventing data.

## Sales → Calendar detail

Left Anti result:

- **771 rows returned**
- **40 distinct non-null unmatched dates**
- **1 null Date**

The non-null unmatched dates were:

- `1/15/2025`
- `6/11/2025`
- `9/1/2025`
- `10/13/2025`
- `1/29/2026`
- `3/9/2026`
- `3/11/2026`
- `4/13/2026`
- `4/25/2026`
- every date from `7/1/2026` through `7/31/2026`

The null Date is a blank value and is not treated as a true orphan key.

## Sales → Customers detail

Raw Left Anti result:

- **5,047 rows**

After separating blank CustomerIDs:

- **5,039 null / blank CustomerIDs**
- **8 true non-null orphan rows**

Distinct true orphan CustomerIDs:

- `C0182`
- `C0183`
- `C0184`

Decision:

- Blank CustomerIDs are treated as valid missing values such as walk-in transactions.
- The 8 true orphan rows are **ESCALATED** because the correct customer references cannot be determined safely.

## Inventory → Calendar detail

Left Anti result:

- **82 orphan rows**

Distinct offending dates:

- `1/15/2025`
- `9/1/2025`

These inventory records were retained because the problem is the missing calendar reference rather than proof that the inventory transactions are invalid.

## Employees → Branches detail

Left Anti result:

- **1 orphan row**

Record:

- EmployeeID: `E004`
- EmployeeName: Bea Ramos
- BranchID: `B07`

Decision: **ACCEPT**

B07 is a real branch identified by the activity as having opened in July, so the employee record remains.

## Blank vs orphan

**Blank:** No value was recorded. A blank CustomerID can represent a walk-in customer who never joined the loyalty programme.

**Orphan:** A value was recorded, but the value points to a reference that does not exist in the related table.

The distinction matters because a blank can be a valid business fact, while an orphan indicates a referential-integrity issue that must be investigated and documented.
