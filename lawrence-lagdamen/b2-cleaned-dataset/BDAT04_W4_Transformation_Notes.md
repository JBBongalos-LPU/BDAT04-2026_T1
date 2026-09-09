# BDAT04 Week 4 — Transformation Notes

## Rebuild and retained Week 3 cleaning decisions

| Step / Decision | Reason | What was discarded or changed |
|---|---|---|
| Removed 23 surplus duplicate `SaleID` records from `tblSales` | These were confirmed surplus duplicates from the Week 3 investigation and were removed as a final cleaning decision. | 23 duplicate sales rows |
| Set `tblSales[Date]` to Date | The field is used as a date key and must have the correct data type for reliable joins. | No rows discarded |
| Set `tblSales[UnitPrice]` to numeric | `UnitPrice` is a numeric measure and needs a numeric type for analysis. | No rows discarded |
| Removed the optional `Check` column from `tblSales` | Week 4 expects the cleaned sales table to return to 9 columns before the July append. | 1 helper/check column |
| Restored the full `tblInventory` table after investigation | Temporary investigation filters were not final cleaning decisions. | No legitimate inventory rows discarded |
| Removed thousand separators from `tblInventory[QuantityMoved]` and set it to Whole Number | This standardized the quantity field so it could be treated as numeric data. | Formatting changed; no valid rows discarded |
| Retained `QuantityMoved = -15` | The value was confirmed as a valid Transfer Out that happened only once, not an error. | Nothing |
| Set `tblInventory[Date]` to Date | The field is used in the Inventory → Calendar integrity check and requires a matching date type. | No rows discarded |
| Set `tblCustomers[JoinedDate]` to Date | The field represents a date and was standardized to the correct type. | No rows discarded |

## Week 4 — July append

| Step / Decision | Reason | What was discarded or changed |
|---|---|---|
| Loaded `tblSalesJul2026` | July sales were supplied as a separate monthly file and needed to be appended to the cleaned sales table. | Nothing |
| Initial append produced 11 columns | `tblSales` used `PaymentMethod` while the July file used `PaymentType`, so Power Query treated them as separate fields. | Nothing; this was diagnosed before the corrected append |
| `Renamed to match tblSales`: `PaymentType` → `PaymentMethod` | Both columns represented the same payment information. Renaming aligned the schemas so the July rows appended into the existing field instead of creating two partially null columns. | Nothing |
| Appended July sales to `tblSales` | Combined the existing 10,566 sales rows with the 601 July rows. | Nothing; final result became 11,167 rows and 9 columns |

## Week 4 — BranchID cleaning decisions

| Step / Decision | Reason | What was discarded or changed |
|---|---|---|
| `FIX - Trim BranchID` | Removed extra/hidden whitespace from recognizable BranchID values such as malformed versions of `B03` and `B06`. | No rows discarded; whitespace only |
| `FIX - Uppercase BranchID` | Standardized lowercase values such as `b01` and `b04` to match valid branch keys. | No rows discarded; text case only |
| `FIX - Standardize BranchID` | Standardized recognizable malformed values such as `B-02` and `B-05` to their matching branch key format. | No rows discarded; formatting only |
| ACCEPT `B07` | After the recognizable formatting fixes, 26 unmatched Sales → Branches rows remained and all used `B07`. The activity identifies B07 as a real branch that opened in July, so the reference table is incomplete rather than the sales being invalid. | Nothing |
| ACCEPT employee `E004` / Bea Ramos with `B07` | The employee record points to the same real B07 branch identified by the activity. | Nothing |

## Week 4 — Other integrity decisions

| Decision | Reason | What was discarded |
|---|---|---|
| ESCALATE `P99` | `P99` appears in 9 sales records but does not exist in `tblProducts`. There is not enough evidence to determine what valid product it should represent without guessing. | Nothing |
| Treat null `CustomerID` values as blanks, not orphans | A blank CustomerID can represent a walk-in customer who never joined the loyalty programme. Missing is not automatically broken. | Nothing |
| ESCALATE `C0182`, `C0183`, and `C0184` | These IDs appear in 8 sales rows but do not exist in `tblCustomers`. Their correct reference cannot be determined safely from the available data. | Nothing |
| Retain unmatched Sales → Calendar records | The unmatched non-null values are dates present in sales but missing from `tblCalendar`; deleting the sales would remove valid business records. The single null Date is treated separately as a blank. | Nothing |
| Retain unmatched Inventory → Calendar records | The 82 inventory rows use `1/15/2025` or `9/1/2025`, both missing from `tblCalendar`. The inventory records were retained rather than silently removed. | Nothing |

## Final model principle

Temporary investigation steps such as diagnostic filters, Remove Duplicates used only to identify distinct offending values, Group By steps, and other scratch-work steps were removed after their results were recorded. The final model keeps the cleaning decisions, not the investigation process.
