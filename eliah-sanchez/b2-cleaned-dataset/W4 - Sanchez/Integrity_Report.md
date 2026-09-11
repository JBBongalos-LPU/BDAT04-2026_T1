# Integrity Report

I tested six relationships in Power Query and recorded the orphan rows I found for each one.

| Relationship | On | Predict | Orphan rows found | Decision |
|---|---|---:|---:|---|
| tblSales → tblBranches | BranchID | 50 | 0 | No action |
| tblSales → tblProducts | ProductID | 10 | 0 | No action |
| tblSales → tblCalendar | Date | 365 | 1202 | Accept |
| tblSales → tblCustomers | CustomerID | 500 | 560 | Check |
| tblInventory → tblCalendar | Date | 100 | 82 | Accept |
| tblEmployees → tblBranches | BranchID | 50 | 1 | Accept |

I tested all six relationships and recorded the number of orphan rows found. I also recorded what I decided to do with each result.
