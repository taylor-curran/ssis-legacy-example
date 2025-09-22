# ssis-legacy-example

## SSIS 2016 Demo Project (Extract → Transform → DQ → Audit)

This project shows common SSIS 2016 patterns you can later port 1:1 into code-first orchestration:
- OLE DB Source from SQL Server
- Derived Column transforms (type conversions, rounding)
- Conditional Split (business filters)
- Aggregation (dedupe by business key)
- Error outputs to quarantine table
- Parameterized run date + batch id
- DQ validation via Execute SQL Task
- Simple audit/lineage rows

## Objects
- Source: dbo.transactions, dbo.customers
- Staging: stage.Stg_Transactions (+ _Err)
- Curated: curated.Cur_Transactions
- Audit: dbo.ETL_Audit

## Quick start
1) Run `sql/00_schema.sql` then `sql/01_seed.sql` in SQL Server.
2) Open `ETL_Proj/ETL_Proj.dtproj` in VS/SSDT (SSIS 2016).
3) Create two OLE DB Connection Managers in the project:
   - `CM_SQL_SRC` → your SQL Server (source objects exist here)
   - `CM_SQL_ETL` → same or another SQL Server (stage/curated/audit)
4) Set project parameter defaults in `Parameters/ETL_Proj.params` if desired.
5) Execute packages in order: 00 → 01 → 02 → 03.

> Note: This repo intentionally focuses on *source-side* logic and SSIS patterns, not any downstream target.
